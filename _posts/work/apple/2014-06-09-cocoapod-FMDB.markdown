---
layout:     post
title:      "FMDB"
subtitle:   " \"FMDB\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - cocoapod
---
https://github.com/ccgus/fmdb

pod 'FMDB'

FMDatabase
FMResultSet
FMDatabaseQueue

//存在打开，不存在则创建
//@“”: 在临时文件夹创建空数据库
//NULL: 内存数据库
FMDatabase *db = [FMDatabase databaseWithPath:@“/tmp/tmp.db"];

if (![db open]) {
    [db release];
    return;
}
NSString *sql = @“CREATE TABLE ‘User’ (‘id’ INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, ‘name’ VARCHAR(30), ‘password’ VARCHAR(30)) ”;
BOOL res = db executeUpdate:sql
if (!res)

//query
FMResultSet *s = [db executeQuery:@"SELECT * FROM myTable"];
while ([s next]) {
    //retrieve values for each record
}

FMResultSet *s = [db executeQuery:@"SELECT COUNT(*) FROM myTable"];
if ([s next]) {
    int totalCount = [s intForColumnIndex:0];
    NSString *pass = [s stringForColumn:@“name”];
}
[db close];




NSString* docsdir = [NSSearchPathForDirectoriesInDomains( NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
NSString* dbpath = [docsdir stringByAppendingPathComponent:@"user.sqlite"];
FMDatabase* db = [FMDatabase databaseWithPath:dbpath];
[db open];
FMResultSet *rs = [db executeQuery:@"select * from people"];
while ([rs next]) {
    NSLog(@"%@ %@",
        [rs stringForColumn:@"firstname"],
        [rs stringForColumn:@"lastname"]);
}
[db close];



