# local log

## Install nuget

```xml
<PackageReference Include="OpenTelemetry" Version="1.4.0-alpha.2" />
<PackageReference Include="OpenTelemetry.Exporter.OpenTelemetryProtocol" Version="1.4.0-alpha.2" />
<PackageReference Include="OpenTelemetry.Extensions.Hosting" Version="1.0.0-rc9.6" />
<PackageReference Include="OpenTelemetry.Instrumentation.AspNetCore" Version="1.0.0-rc9.6" />
<PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.0.0-rc9.6" />
<PackageReference Include="OpenTelemetry.Exporter.Console" Version="1.4.0-alpha.2" />
<PackageReference Include="prometheus-net" Version="6.0.0" />
<PackageReference Include="prometheus-net.AspNetCore" Version="6.0.0" />
<PackageReference Include="prometheus-net.AspNetCore.HealthChecks" Version="6.0.0" />
<PackageReference Include="Serilog.AspNetCore" Version="6.1.0" />
<PackageReference Include="Serilog.Enrichers.Span" Version="3.1.0" />
<PackageReference Include="Serilog.Extensions.Hosting" Version="5.0.1" />
<PackageReference Include="Serilog.Sinks.Grafana.Loki" Version="7.1.1" />
```

## add logging

```cs
.UseSerilog((host, log) =>
{
    if (host.HostingEnvironment.IsProduction())
        log.MinimumLevel.Information();
    else
        log.MinimumLevel.Verbose();

    log.Enrich.WithSpan();
    log.Enrich.FromLogContext();
    log.Enrich.WithProperty("ApplicationName", "WalletApi");
    log.MinimumLevel.Override("Microsoft", LogEventLevel.Warning);
    log.MinimumLevel.Override("Quartz", LogEventLevel.Information);

    log.WriteTo.GrafanaLoki("http://localhost:3100") // address to loki server
        .WriteTo.Console(new RenderedCompactJsonFormatter());

})
```

## Add Otel

https://opentelemetry.io/docs/instrumentation/net/