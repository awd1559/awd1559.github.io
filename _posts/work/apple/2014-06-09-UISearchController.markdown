---
layout:     post
title:      "UISearchController"
subtitle:   " \"UISearchController\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - iOS
---

```
MainViewController : UITableViewController<UISearchControllerDelegate, UISearchBarDelegate, UISearchResultsUpdating>
	UISearchController* searchController;
	ResultsTableController* resultsTableController;
	
viewDidLoad
	resultsTableController = ResultsTableController alloc init;
	resultsTableController.tableView.delegate  = self;

	searchController = UISearchController alloc initWithSearchResultsController:resultViewController
	searchController.delegate = self;	

	searchController.searchBar sizeToFit
	searchController.searchBar.delegate = self;		//UISearchBarDelegate
	self.tableView.tableHeaderView = searchController.searchBar;

#pragma mark UISearchBarDelegate
- (void)searchBarSearchButtonClicked:(UISearchBar *)searchBar {
    [searchBar resignFirstResponder];
}

#pragma mark UISearchControllerDelegate
- (void)presentSearchController:(UISearchController *)searchController {}
- (void)willPresentSearchController:(UISearchController *)searchController {}
- (void)didPresentSearchController:(UISearchController *)searchController {}
- (void)willDismissSearchController:(UISearchController *)searchController {}
- (void)didDismissSearchController:(UISearchController *)searchController {}

#pragma mark UISearchResultsUpdating
- (void)updateSearchResultsForSearchController:(UISearchController *)searchController


ResultsTableController : UITableController
```