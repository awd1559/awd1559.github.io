Architecture
NSURLConnection
	◦	AFURLConnectionOperation
	◦	AFHTTPRequestOperation
	◦	AFHTTPRequestOperationManager
NSURLSession (iOS 7 / Mac OS X 10.9)
	◦	AFURLSessionManager
	◦	AFHTTPSessionManager
Serialization
	◦	<AFURLRequestSerialization>
	▪	AFHTTPRequestSerializer
	▪	AFJSONRequestSerializer
	▪	AFPropertyListRequestSerializer
	◦	<AFURLResponseSerialization>
	▪	AFHTTPResponseSerializer
	▪	AFJSONResponseSerializer
	▪	AFXMLParserResponseSerializer
	▪	AFXMLDocumentResponseSerializer (Mac OS X)
	▪	AFPropertyListResponseSerializer
	▪	AFImageResponseSerializer
	▪	AFCompoundResponseSerializer
Additional Functionality
	◦	AFSecurityPolicy
	◦	AFNetworkReachabilityManager
Usage
HTTP Request Operation Manager
AFHTTPRequestOperationManager encapsulates the common patterns of communicating with a web application over HTTP, including request creation, response serialization, network reachability monitoring, and security, as well as request operation management.
GET Request
AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
[manager GET:@"http://example.com/resources.json" parameters:nil success:^(AFHTTPRequestOperation *operation, id responseObject) {
    NSLog(@"JSON: %@", responseObject);
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
    NSLog(@"Error: %@", error);
}];
POST URL-Form-Encoded Request
AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
NSDictionary *parameters = @{@"foo": @"bar"};
[manager POST:@"http://example.com/resources.json" parameters:parameters success:^(AFHTTPRequestOperation *operation, id responseObject) {
    NSLog(@"JSON: %@", responseObject);
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
    NSLog(@"Error: %@", error);
}];
POST Multi-Part Request
AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
NSDictionary *parameters = @{@"foo": @"bar"};
NSURL *filePath = [NSURL fileURLWithPath:@"file://path/to/image.png"];
[manager POST:@"http://example.com/resources.json" parameters:parameters constructingBodyWithBlock:^(id<AFMultipartFormData> formData) {
    [formData appendPartWithFileURL:filePath name:@"image" error:nil];
} success:^(AFHTTPRequestOperation *operation, id responseObject) {
    NSLog(@"Success: %@", responseObject);
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
    NSLog(@"Error: %@", error);
}];

AFURLSessionManager
AFURLSessionManager creates and manages an NSURLSession object based on a specified NSURLSessionConfiguration object, which conforms to <NSURLSessionTaskDelegate>, <NSURLSessionDataDelegate>, <NSURLSessionDownloadDelegate>, and <NSURLSessionDelegate>.
Creating a Download Task
NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
AFURLSessionManager *manager = [[AFURLSessionManager alloc] initWithSessionConfiguration:configuration];

NSURL *URL = [NSURL URLWithString:@"http://example.com/download.zip"];
NSURLRequest *request = [NSURLRequest requestWithURL:URL];

NSURLSessionDownloadTask *downloadTask = [manager downloadTaskWithRequest:request progress:nil destination:^NSURL *(NSURL *targetPath, NSURLResponse *response) {
    NSURL *documentsDirectoryURL = [[NSFileManager defaultManager] URLForDirectory:NSDocumentDirectory inDomain:NSUserDomainMask appropriateForURL:nil create:NO error:nil];
    return [documentsDirectoryURL URLByAppendingPathComponent:[response suggestedFilename]];
} completionHandler:^(NSURLResponse *response, NSURL *filePath, NSError *error) {
    NSLog(@"File downloaded to: %@", filePath);
}];
[downloadTask resume];
Creating an Upload Task
NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
AFURLSessionManager *manager = [[AFURLSessionManager alloc] initWithSessionConfiguration:configuration];

NSURL *URL = [NSURL URLWithString:@"http://example.com/upload"];
NSURLRequest *request = [NSURLRequest requestWithURL:URL];

NSURL *filePath = [NSURL fileURLWithPath:@"file://path/to/image.png"];
NSURLSessionUploadTask *uploadTask = [manager uploadTaskWithRequest:request fromFile:filePath progress:nil completionHandler:^(NSURLResponse *response, id responseObject, NSError *error) {
    if (error) {
        NSLog(@"Error: %@", error);
    } else {
        NSLog(@"Success: %@ %@", response, responseObject);
    }
}];
[uploadTask resume];
Creating an Upload Task for a Multi-Part Request, with Progress
NSMutableURLRequest *request = [[AFHTTPRequestSerializer serializer] multipartFormRequestWithMethod:@"POST" URLString:@"http://example.com/upload" parameters:nil constructingBodyWithBlock:^(id<AFMultipartFormData> formData) {
        [formData appendPartWithFileURL:[NSURL fileURLWithPath:@"file://path/to/image.jpg"] name:@"file" fileName:@"filename.jpg" mimeType:@"image/jpeg" error:nil];
    } error:nil];

AFURLSessionManager *manager = [[AFURLSessionManager alloc] initWithSessionConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]];
NSProgress *progress = nil;

NSURLSessionUploadTask *uploadTask = [manager uploadTaskWithStreamedRequest:request progress:&progress completionHandler:^(NSURLResponse *response, id responseObject, NSError *error) {
    if (error) {
        NSLog(@"Error: %@", error);
    } else {
        NSLog(@"%@ %@", response, responseObject);
    }
}];

[uploadTask resume];
Creating a Data Task
NSURLSessionConfiguration *configuration = [NSURLSessionConfiguration defaultSessionConfiguration];
AFURLSessionManager *manager = [[AFURLSessionManager alloc] initWithSessionConfiguration:configuration];

NSURL *URL = [NSURL URLWithString:@"http://example.com/upload"];
NSURLRequest *request = [NSURLRequest requestWithURL:URL];

NSURLSessionDataTask *dataTask = [manager dataTaskWithRequest:request completionHandler:^(NSURLResponse *response, id responseObject, NSError *error) {
    if (error) {
        NSLog(@"Error: %@", error);
    } else {
        NSLog(@"%@ %@", response, responseObject);
    }
}];
[dataTask resume];

Request Serialization
Request serializers create requests from URL strings, encoding parameters as either a query string or HTTP body.
NSString *URLString = @"http://example.com";
NSDictionary *parameters = @{@"foo": @"bar", @"baz": @[@1, @2, @3]};
Query String Parameter Encoding
[[AFHTTPRequestSerializer serializer] requestWithMethod:@"GET" URLString:URLString parameters:parameters error:nil];
GET http://example.com?foo=bar&baz[]=1&baz[]=2&baz[]=3
URL Form Parameter Encoding
[[AFHTTPRequestSerializer serializer] requestWithMethod:@"POST" URLString:URLString parameters:parameters];
POST http://example.com/
Content-Type: application/x-www-form-urlencoded

foo=bar&baz[]=1&baz[]=2&baz[]=3
JSON Parameter Encoding
[[AFJSONRequestSerializer serializer] requestWithMethod:@"POST" URLString:URLString parameters:parameters];
POST http://example.com/
Content-Type: application/json

{"foo": "bar", "baz": [1,2,3]}

Network Reachability Manager
AFNetworkReachabilityManager monitors the reachability of domains, and addresses for both WWAN and WiFi network interfaces.
	◦	Do not use Reachability to determine if the original request should be sent.
	▪	You should try to send it.
	◦	You can use Reachability to determine when a request should be automatically retried.
	▪	Although it may still fail, a Reachability notification that the connectivity is available is a good time to retry something.
	◦	Network reachability is a useful tool for determining why a request might have failed.
	▪	After a network request has failed, telling the user they're offline is better than giving them a more technical but accurate error, such as "request timed out."
See also WWDC 2012 session 706, "Networking Best Practices.".
Shared Network Reachability
[[AFNetworkReachabilityManager sharedManager] setReachabilityStatusChangeBlock:^(AFNetworkReachabilityStatus status) {
    NSLog(@"Reachability: %@", AFStringFromNetworkReachabilityStatus(status));
}];

[[AFNetworkReachabilityManager sharedManager] startMonitoring];
HTTP Manager Reachability
NSURL *baseURL = [NSURL URLWithString:@"http://example.com/"];
AFHTTPRequestOperationManager *manager = [[AFHTTPRequestOperationManager alloc] initWithBaseURL:baseURL];

NSOperationQueue *operationQueue = manager.operationQueue;
[manager.reachabilityManager setReachabilityStatusChangeBlock:^(AFNetworkReachabilityStatus status) {
    switch (status) {
        case AFNetworkReachabilityStatusReachableViaWWAN:
        case AFNetworkReachabilityStatusReachableViaWiFi:
            [operationQueue setSuspended:NO];
            break;
        case AFNetworkReachabilityStatusNotReachable:
        default:
            [operationQueue setSuspended:YES];
            break;
    }
}];

[manager.reachabilityManager startMonitoring];

Security Policy
AFSecurityPolicy evaluates server trust against pinned X.509 certificates and public keys over secure connections.
Adding pinned SSL certificates to your app helps prevent man-in-the-middle attacks and other vulnerabilities. Applications dealing with sensitive customer data or financial information are strongly encouraged to route all communication over an HTTPS connection with SSL pinning configured and enabled.
Allowing Invalid SSL Certificates
AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
manager.securityPolicy.allowInvalidCertificates = YES; // not recommended for production

AFHTTPRequestOperation
AFHTTPRequestOperation is a subclass of AFURLConnectionOperation for requests using the HTTP or HTTPS protocols. It encapsulates the concept of acceptable status codes and content types, which determine the success or failure of a request.
Although AFHTTPRequestOperationManager is usually the best way to go about making requests, AFHTTPRequestOperation can be used by itself.
GET with AFHTTPRequestOperation
NSURL *URL = [NSURL URLWithString:@"http://example.com/resources/123.json"];
NSURLRequest *request = [NSURLRequest requestWithURL:URL];
AFHTTPRequestOperation *op = [[AFHTTPRequestOperation alloc] initWithRequest:request];
op.responseSerializer = [AFJSONResponseSerializer serializer];
[op setCompletionBlockWithSuccess:^(AFHTTPRequestOperation *operation, id responseObject) {
    NSLog(@"JSON: %@", responseObject);
} failure:^(AFHTTPRequestOperation *operation, NSError *error) {
    NSLog(@"Error: %@", error);
}];
[[NSOperationQueue mainQueue] addOperation:op];
Batch of Operations
NSMutableArray *mutableOperations = [NSMutableArray array];
for (NSURL *fileURL in filesToUpload) {
    NSURLRequest *request = [[AFHTTPRequestSerializer serializer] multipartFormRequestWithMethod:@"POST" URLString:@"http://example.com/upload" parameters:nil constructingBodyWithBlock:^(id<AFMultipartFormData> formData) {
        [formData appendPartWithFileURL:fileURL name:@"images[]" error:nil];
    }];

    AFHTTPRequestOperation *operation = [[AFHTTPRequestOperation alloc] initWithRequest:request];

    [mutableOperations addObject:operation];
}

NSArray *operations = [AFURLConnectionOperation batchOfRequestOperations:@[...] progressBlock:^(NSUInteger numberOfFinishedOperations, NSUInteger totalNumberOfOperations) {
    NSLog(@"%lu of %lu complete", numberOfFinishedOperations, totalNumberOfOperations);
} completionBlock:^(NSArray *operations) {
    NSLog(@"All operations in batch complete");
}];
[[NSOperationQueue mainQueue] addOperations:operations waitUntilFinished:NO];
Unit Tests
AFNetworking includes a suite of unit tests within the Tests subdirectory. In order to run the unit tests, you must install the testing dependencies via CocoaPods:
$ cd Tests
$ pod install
Once testing dependencies are installed, you can execute the test suite via the 'iOS Tests' and 'OS X Tests' schemes within Xcode.
Running Tests from the Command Line
Tests can also be run from the command line or within a continuous integration environment. The xcpretty utility needs to be installed before running the tests from the command line:
$ gem install xcpretty
Once xcpretty is installed, you can execute the suite via rake test.




//install
platform :ios, '8.0'

pod 'AFNetworking', '~> 3.0'


