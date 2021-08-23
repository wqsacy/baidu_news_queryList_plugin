# QueryList-Rule-Baidu
QueryList Plugin: Baidu News searcher. 

QueryList插件：百度搜索引擎

> QueryList:[https://github.com/jae-jae/QueryList](https://github.com/jae-jae/QueryList)

## Installation for QueryList4
```
composer require wangqs/querylist-rule-baidu-news
```

## API
- BaiduNews **baidu($pageNumber = 10)**:get BaiduNews Searcher.

class **BaiduNews**:
- BaiduNews **search($keyword)**:set search keyword.
- BaiduNews **setHttpOpt(array $httpOpt = [])**：Set the http option,see: [GuzzleHttp options](http://docs.guzzlephp.org/en/stable/request-options.html)
- int **getCount()**:Get the total number of search results.
- int **getCountPage()**:Get the total number of pages.
- Collection **page($page = 1,$realURL = false)**:Get search results

## Usage
- Installation Plugin

```php
use QL\QueryList;
use QL\Ext\BaiduNews;

$ql = QueryList::getInstance();
$ql->use(BaiduNews::class);
//or Custom function name
$ql->use(BaiduNews::class,'baidu');
```
- Example-1

```php
$baiduNews = $ql->baiduNews(10)
$searcher = $baiduNews->search('QueryList');
$count = $searcher->getCount();
$data = $searcher->page(1);
$data = $searcher->page(2);

$searcher = $baiduNews->search('php');
$countPage = $searcher->getCountPage();
for ($page = 1; $page <= $countPage; $page++)
{
    $data = $searcher->page($page);
}
```

- Example-2

```php
$searcher = $ql->baiduNews()->search('QueryList');
$data = $searcher->setHttpOpt([
    // Set the http proxy
    'proxy' => 'http://222.141.11.17:8118',
   // Set the timeout time in seconds
    'timeout' => 30,
])->page(1);
```

- Example-3

```php
$baiduNews = $ql->baiduNews(3)
$searcher = $baiduNews->search('QueryList');

$data = $searcher->page(1);
print_r($data->all());

// Get real url
$data = $searcher->page(1,true);
print_r($data->all());

