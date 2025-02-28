### 说明

- 这是一个基于PlayWright的Unofficial Bing Search API简单实现，用于SemanticKernel.Plugins.Web中测试使用。当然也可直接使用。

- 使用前需安装PlayWright，参考[Installation | Playwright](https://playwright.dev/docs/intro#installing-playwright)



### 基本使用

- SemanticKernel.Plugins.Web使用方式

```cs
var textSearch = new ShaBingSearch();
var query = "什么是语义内核？";
KernelSearchResults<object> objectResults = await textSearch.GetSearchResultsAsync(
    query,
    new() { Top = 4 }
);
await foreach (ShaBingWebPage webPage in objectResults.Results)
{
    Console.WriteLine($"名称:            {webPage.Name}");
    Console.WriteLine($"摘要:         {webPage.Snippet}");
    Console.WriteLine($"网址:             {webPage.Url}");
    Console.WriteLine($"显示网址:      {webPage.DisplayUrl}");
    Console.WriteLine($"最后爬取日期: {webPage.DateLastCrawled}");
}
```

- 直接使用

```cs
using var bingSearch = new ShaBingSearchCore();
var results = await bingSearch.ExecuteSearchAsync(
    "什么是语义内核？", 
    new Microsoft.SemanticKernel.Data.TextSearchOptions() { Top = 10 }
);
Console.WriteLine(JsonSerializer.Serialize(results, new JsonSerializerOptions
{
    Encoder = JavaScriptEncoder.UnsafeRelaxedJsonEscaping,
    WriteIndented = true
}));
```

