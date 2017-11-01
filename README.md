Our CMS : .net + MongoDB = ❤
=================

You can get the latest stable release from the official Nuget.org feed or from our github releases page.

Getting Started
---------------

### Step 1: Add Our CMS
```C#
using our.cms;
```

```C#
public void ConfigureServices(IServiceCollection services)
{
...
services.AddOurCMS();
...
}
```

```C#
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ...
{
...
app.UseOurCMS();
...
}
```

### Step 2: Create Model
```C#
[Root]
[ParentOf(typeof(Child))]
public class Root : CmsEntry
{
}

public class Child : CmsEntry
{
  [Legend]
  [Text]
  public string Title { get; set; }
  
  [HTML]
  public string Content { get; set; }
}
```

### Step 2: Use Data
```C#
public class HomeController : Controller
{
  
  protected readonly DB DB;
  
  // inject the database provider using D.I.
  public HomeController(IDBProvider dbprovider) {
    // gets the database
    DB = dbprovider.Default;
  }
  ...
  public IActionResult Index()
  {
    
    var child = DB.Find<Child>().FirstOrDefault();
    
    
    
    ViewData["Title"] = child?.Title ?? "no child !";
    ViewData["Content"] = child?.Content ?? "";
    
    return View();
  }
```


