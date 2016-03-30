---
layout:     post
title:      "table"
subtitle:   " \"UITableView\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---

viewDidLoad
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:@“Cell"];



MyTableViewController : UITableViewController
-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
-(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
-(CGFloat)tableView:(nonnull UITableView *)tableView heightForRowAtIndexPath:(nonnull NSIndexPath *)indexPath
-(UITableViewCell*)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath



-(CGFloat)tableView:(UITableView*)tableview heightForHeaderInSection:(NSInteger)section
-(UIView*)tableView:(UITableView*)tableview viewForHeaderInSection:(NSInteger)section
-(CGFloat)tableView:(UITableView*)tableview heightForFooterInSection:(NSInteger)section
-(UIView*)tableView:(UITableView*)tableview viewForFooterInSection:(NSInteger)section

代码方式初始化一个TableViewController
- (instancetype)init
{
    self = [super initWithStyle:UITableViewStyleGrouped];
    if (self) {
        self.persons =  [[NSMutableArray alloc] initWithObjects:@"1111", @"2222", @"3333", @"4444", @"5555", @"6666", nil];//初始化数据
    }
    return self;
}
- (void)viewDidLoad {
    [super viewDidLoad];
    
    [self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:@“Cell"]; 				  //注册重用标识
    
    UIView* header = self.headerView;
    [self.tableView setTableHeaderView: header];								//设定TableView的head
}

headerview可以从xib中来
-(UIView*)headerView{
    if (!_headerView) {
        // Load HeaderView.xib
        [[NSBundle mainBundle] loadNibNamed:@"headerview"
                                      owner:self				//讲xib文件的FileOwner设为当前ViewController				
                                    options:nil];
    }
    return _headerView;
}
定义表UI
#pragma mark --UITableViewDataSource 协议方法
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return [self.listTeams count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *CellIdentifier = @"CellIdentifier";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    if (cell == nil) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:CellIdentifier];
    }

    NSUInteger row = [indexPath row];
    NSDictionary *rowDict = [self.listTeams objectAtIndex:row];
    cell.textLabel.text =  [rowDict objectForKey:@"name"];
    
    NSString *imagePath = [rowDict objectForKey:@"image"];
    imagePath = [imagePath stringByAppendingString:@".png"];
    cell.imageView.image = [UIImage imageNamed:imagePath];
    
    cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
    
    return cell;
}


定义表UI－自定义table view cell
如果使用storyboard，拖入UITableViewCell
CustomCell : UITableViewCell
@property(weak, nonatomic) IBOutlet UILable *name;
@property(weak, nonatomic) IBOutlet UIImageView *image;

CustomCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];

#pragma mark - UICollectionViewDelegate
- (void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath
{
    NSDictionary *event = [self.events objectAtIndex:(indexPath.section*2 + indexPath.row)];
    NSLog(@"select event name : %@", [event objectForKey:@"name"]);
}
按钮切换UITableViewController编辑模式
- (IBAction)toggleEditingMode:(id)sender {
    // If you are currently in editing mode...
    if (self.isEditing) {
        // Change text of button to inform user of state
        [sender setTitle:@"编辑" forState:UIControlStateNormal];
        
        // Turn off editing mode
        [self setEditing:NO animated:YES];
    } else {
        // Change tet of button to inform user of state
        [sender setTitle:@"完成" forState:UIControlStateNormal];
        
        // Enter editing mode
        [self setEditing:YES animated:YES];
    }
}


tableView: commitEditingStyle:(UITableViewCellEditingStyle) forRowAtIndexPath(NSIndexPath*)
self.tableView deleteRowAtIndexPaths: withRowAnimation:表编辑－增加
NSString *item = [NSString stringWithFormat:@“”];
self.list insertObject:item atIndex:
NSIndexpath *indexPath = [NSIndexPath indexPathForRow:0 inSection:0];   //构造表上的位置
[self.tableView insertRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationTop];
表编辑－move
UITableViewDataSource
实现如下函数即可在编辑模式下移动UITableViewCell
- (void)   tableView:(UITableView *)tableView
  moveRowAtIndexPath:(NSIndexPath *)sourceIndexPath
         toIndexPath:(NSIndexPath *)destinationIndexPath
{
    Item *item = data[sourceIndex]
    //调换data中数据位置
}

表编辑－删除
UITableViewDataSource
- (void)   tableView:(UITableView *)tableView
  commitEditingStyle:(UITableViewCellEditingStyle)editingStyle
   forRowAtIndexPath:(NSIndexPath *)indexPath
{
    // If the table view is asking to commit a delete command...
    if (editingStyle == UITableViewCellEditingStyleDelete) {
        [self.persons removeObjectAtIndex:indexPath.row];
        
        // Also remove that row from the table view with an animation
        [tableView deleteRowsAtIndexPaths:@[indexPath]
                         withRowAnimation:UITableViewRowAnimationFade];
    }
}





Navigation to Detail
比使用自定义view作为table的header View更好的方法
MyTableViewController *mycontroller = [[MyTableViewController alloc] init];
UINavigationController *nav = [[UINavigationController alloc] initWithRootViewController:mycontroller];
self.window.rootViewController = nav;


MyTableViewController : UITableViewController
- (instancetype)init
{
        self.persons =  [[NSMutableArray alloc] initWithObjects:@"1111", @"2222", @"3333", @"4444", @"5555", @"6666", nil];
        
        UINavigationItem *navitem = self.navigationItem;
        navitem.title = @"MyTableTitle";
        
        UIBarButtonItem *right = [[UIBarButtonItem alloc] initWithBarButtonSystemItem:UIBarButtonSystemItemAdd target:self action:@selector(addItem:)];
        navitem.rightBarButtonItem = right;
        navitem.leftBarButtonItem = self.editButtonItem;
}

//navigate to detailViewController
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    DetailViewController *detailViewController = [[DetailViewController alloc] init];
   
    NSString* item = self.persons[indexPath.row]; 
   detailViewController.message = item;
    
    [self.navigationController pushViewController:detailViewController
                                         animated:YES];
}



UITableView中放入UISearchBar and Search Display Controller
#pragma mark --UISearchBarDelegate 协议方法
- (void)searchBarCancelButtonClicked:(UISearchBar *)searchBar
{
    //查询所有
    [self filterContentForSearchText:@"" scope:-1];
}

#pragma mark - UISearchDisplayDelegate Methods
//当文本内容发生改变时候，向表视图数据源发出重新加载消息
- (BOOL)searchDisplayController:(UISearchDisplayController *)controller shouldReloadTableForSearchString:(NSString *)searchString
{
    [self filterContentForSearchText:searchString scope:self.searchBar.selectedScopeButtonIndex];
    //YES情况下表视图可以重新加载
    return YES;
}

// 当Scope Bar选择发送变化时候，向表视图数据源发出重新加载消息
- (BOOL)searchDisplayController:(UISearchDisplayController *)controller shouldReloadTableForSearchScope:(NSInteger)searchOption
{
    [self filterContentForSearchText:self.searchBar.text scope:searchOption];
    // YES情况下表视图可以重新加载
    return YES;
}

#pragma mark Content Filtering
- (void)filterContentForSearchText:(NSString*)searchText scope:(NSUInteger)scope;
{
    
    if([searchText length]==0)
    {
        //查询所有
        self.listFilterTeams = [NSMutableArray arrayWithArray:self.listTeams];
        return;
    }
    
    NSPredicate *scopePredicate;
    NSArray *tempArray ;
    
    switch (scope) {
        case 0: //英文
            scopePredicate = [NSPredicate predicateWithFormat:@"SELF.name contains[c] %@",searchText];
            tempArray =[self.listTeams filteredArrayUsingPredicate:scopePredicate];
            self.listFilterTeams = [NSMutableArray arrayWithArray:tempArray];

            break;
        case 1:
            scopePredicate = [NSPredicate predicateWithFormat:@"SELF.image contains[c] %@",searchText];
            tempArray =[self.listTeams filteredArrayUsingPredicate:scopePredicate];
            self.listFilterTeams = [NSMutableArray arrayWithArray:tempArray];

            break;
        default:
            //查询所有
            self.listFilterTeams = [NSMutableArray arrayWithArray:self.listTeams];
            break;
    }
}


下拉刷新
UITableViewController
//初始化UIRefreshControl
UIRefreshControl *rc = [[UIRefreshControl alloc] init];
rc.attributedTitle = [[NSAttributedString alloc]initWithString:@"下拉刷新"];
[rc addTarget:self action:@selector(refreshTableView) forControlEvents:UIControlEventValueChanged];
self.refreshControl = rc;

-(void) refreshTableView
{
    if (self.refreshControl.refreshing) {
        self.refreshControl.attributedTitle = [[NSAttributedString alloc]initWithString:@"加载中..."];
        //添加新的模拟数据
        NSDate *date = [[NSDate alloc] init];
        //模拟请求完成之后，回调方法callBackMethod
        [self performSelector:@selector(callBackMethod:) withObject:date afterDelay:3];
    }
}

//这是一个模拟方法，请求完成之后，回调方法
-(void)callBackMethod:(id) obj
{
    [self.refreshControl endRefreshing];
    self.refreshControl.attributedTitle = [[NSAttributedString alloc]initWithString:@"下拉刷新"];
    [self.Logs addObject:(NSDate*)obj];
    
    [self.tableView reloadData];
}





UITableViewDataSource协议
tableView:cellForRowAtIndexPath:				返回cell
tableView:numberOfRowsInSection:				某个section中的行数
tableView:titleForHeaderInSection:				section的hader
tableView:titleForFooterInSection:				section的footer
numberOfSectionsInTableView:				section的个数
sectionIndexTitlesForTableView:				section的索引标题
tableView:commitEditingStyles:forRowAtIndexPath:		为删除或修改提供数据


UITableViewDelegate协议
tableView:viewForHeaderInSection:				section的Header：UITableViewHeaderFooterView
tableView:viewForFooterInSection:				section的Footer：UITableViewHeaderFooterView
tableView:didEndDisplayingHeaderView:forSection:		Header消失时触发
tableView:didEndDisplayingFooterView:forSection:		Footer消失时触发
tableView:didEndDisplayingCell:forRowAtIndexPath:		Cell消失时触发
tableView:didSelectRowAtIndexPath:				选中Cell时


