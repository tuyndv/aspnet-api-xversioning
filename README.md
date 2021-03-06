**ASP.NET Core (Microsoft.AspNetCore.Mvc.Versioning)**

  * Adds service API versioning to your ASP.NET Core applications
* Support Major.Minor.Build Version (x.x.x)
* Support Get LastVersionApi

 * [![NuGet Release](https://img.shields.io/nuget/vpre/Alomso.AspNetCore.Mvc.Versioning.svg?maxAge=2592000)](https://www.nuget.org/packages/Alomso.AspNetCore.Mvc.Versioning/)

---
**Documentation**

**1. Version Format**

Version Format                               | Example                | Interpretation
---------------------------------------------| ---------------------- | ------------------------------------------
{groupVersion}                               | 2013-03-21, 2012-12-01 | 3.3, 1.2
{majorVersion}                               | 3                      | 3.0
{majorVersion}.{minorVersion}                | 1.2                    | 1.2
{majorVersion}.{minorVersion}.{buildVersion} | 1.2.2                  | 1.2.2



**2. Startup.cs**
```csharp
 services.AddApiVersioning( o =>
            {
                o.AssumeDefaultVersionWhenUnspecified = true;
                o.ReportApiVersions = true;
                o.DefaultApiVersion = new ApiVersion( 1, 2, 2 );
                o.SupportLastVersionApi = true;
            } );
```


**3. ValuesController.cs**
```csharp
namespace Microsoft.Examples.Controllers
{
    [ApiVersion( "1.0" )]
    [ApiVersion( "1.1" )]
    [ApiVersion( "1.0.1" )]
    [ApiVersion( "1.0.2" )]
    [ApiVersion( "1.2" )]
    [ApiVersion( "1.2.2" )]
    [Route( "api/[controller]" )]
    public class ValuesController : Controller
    {
        // GET api/values?api-version=1.0
        [HttpGet, MapToApiVersion( "1.0" )]
        public string GetV1() => $"Controller = {GetType().Name}\nVersion V1.0";

        [HttpGet, MapToApiVersion( "1.1" )]
        public string GetV11() => $"Controller = {GetType().Name}\nVersion V1.1";

        [HttpGet, MapToApiVersion( "1.0.1" )]
        public string GetV101() => $"Controller = {GetType().Name}\nVersion V1.0.1";

        [HttpGet, MapToApiVersion( "1.0.2" )]
        public string GetV102() => $"Controller = {GetType().Name}\nVersion V1.0.2";

        [HttpGet, MapToApiVersion( "1.2" )]
        public string GetV12() => $"Controller = {GetType().Name}\nVersion V1.2";

        [HttpGet, MapToApiVersion( "1.2.2" )]
        public string GetV122() => $"Controller = {GetType().Name}\nVersion V1.2.2";
    }
}
```

