Our CMS :
.net + MongoDB = ❤
=================

You can get the latest stable release from the official Nuget.org feed or from our github releases page.

### Supported Platforms
* .NET Standard 1.6 : [.NET Core 1.0, .NET Framework 4.6.1, Mono 4.6...](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)
* .NET Standard 2.0 : [.NET Core 2.0, .NET Framework 4.6.1, Mono 5.4...](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)

Installation
---------------

### Install nuget
Download via [Nuget](https://www.nuget.org/packages/our.cms/) on `Package Manager Console`:
```
PM> Install-Package our.cms
```

### Add to your app
```C#
using our.cms;
```

```C#
public void ConfigureServices(IServiceCollection services)
{
  …
  services.AddOurCMS();
  …
}
```

```C#
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ...
{
  …
  app.UseOurCMS();
  …
}
```

Getting Started
---------------

### Step 1: Create Model
```C#
using our.cms;
```

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
using our.cms;
```

```C#
public class HomeController : Controller
{
  
  protected readonly DB DB;
  
  // inject the database provider using D.I.
  public HomeController(IDBProvider dbprovider) {
    // gets the database
    DB = dbprovider.Default;
  }
  
  …
  
  public IActionResult Index()
  {
    
    var child = DB.Find<Child>().FirstOrDefault();
    
    ViewData["Title"] = child?.Title ?? "no child !";
    ViewData["Content"] = child?.Content ?? "";
    
    return View();
  }
  
  …
  
}
```


