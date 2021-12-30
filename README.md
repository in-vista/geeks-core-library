# GeeksCoreLibrary (GCL)
[![Build and test](https://github.com/happy-geeks/geeks-core-library/actions/workflows/build-and-test.yml/badge.svg)](https://github.com/happy-geeks/geeks-core-library/actions/workflows/build-and-test.yml)
## Requirements
1. Install .NET Hosting bundle on the server that is running the GCL: https://dotnet.microsoft.com/download/dotnet/5.0

## Using the GCL in a project
To use the GCL in your project, install the NuGet package `GeeksCoreLibrary` and then modify your Startup.cs to look like this:
```C#
public class Startup
{
    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public IConfiguration Configuration { get; }

    // This method gets called by the runtime. Use this method to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddGclServices(Configuration);
        services.AddControllersWithViews();
    }

    // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseGclMiddleware(env);
    }
}
```
If you're creating a new project, we recommend using the [template](https://github.com/happy-geeks/Gcl-Template) for that.

## Configuration
For the GCL to work, you need to set some values in the `appSettings.json`:
```json
{
  "GCL": {
    "connectionString": "", // The connection string to the main database for Wiser.
    "DefaultEncryptionKey": "", // The default encryption key that should be used for encrypting values with AES when no encryption key is given.
    "DefaultEncryptionKeyTripleDes": "",  // The default encryption key that should be used for encrypting values with Tripe DES when no encryption key is given.
    "evoPdfLicenseKey": "" // If you're going to use the PdfService, you need a license key for Evo PDF, or make your own implementation.
  }
}
```
