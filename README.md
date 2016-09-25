# Serilog.Sinks.MySQL
Serilog sink that writes to MySQL database.

## Getting started

Install [Serilog.Sinks.MySQL](#) from NuGet

```PowerShell
Install-Package Serilog.Sinks.MySQL
```

Configure logger by calling WriteTo.MySQL

```C#
var logger = new LoggerConfiguration()
    .WriteTo.MySQL("server=127.0.0.1;uid=user;pwd=password;database=diagnostics;")
    .CreateLogger();

logger.Information("This informational message will be written to MySQL database");
```

## XML <appSettings> configuration

To use the rolling file sink with the [Serilog.Settings.AppSettings](https://www.nuget.org/packages/Serilog.Settings.AppSettings) package, first install that package if you haven't already done so:

```PowerShell
Install-Package Serilog.Settings.AppSettings
```
In your code, call `ReadFrom.AppSettings()`

```C#
var logger = new LoggerConfiguration()
    .ReadFrom.AppSettings()
    .CreateLogger();
```

In your application's App.config or Web.config file, specify the MySQL sink assembly and required **connectionString** under the `<appSettings>` node:

```XML
<appSettings>
    <add key="serilog:using:MySQL" value="Serilog.Sinks.MySQL"/>
    <add key="serilog:write-to:MySQL.connectionString" value="..."/>
    <add key="serilog:write-to:MySQL.tableName" value="Logs"/>
    <add key="serilog:write-to:MySQL.storeTimestampInUtc" value="true"/>
</appSettings>    
```

## Performance
Sink buffers log messages internally and flush to MySQL database in batches using available hardware threads.
