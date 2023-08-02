# CAP.MQTT

Implementation of MQTT plugin for DotNetCore.CAP   
   
DotNetCore.CAP 的 MQTT 插件简易实现   

## Quick Start

### Installation
```csharp
dotnet add package DotNetCore.CAP
dotnet add package DotNetCore.CAP.InMemoryStorage
dotnet add package ASH.CAP.MQTT --version 1.0.0
```

In Startup.cs ，add the following configuration:
```csharp
services.AddCap(x => {
    x.ConsumerThreadCount = 1;
    x.UseMQTT(o => {
        o.HostName = "test.example.com";
        o.UserName = "test";
        o.Password = "test";
        o.ClientId = "cap test client";
    });
    x.UseInMemoryStorage();
});
```

### Process Message / Subscribe Message
```csharp
public class ConsumerController : Controller {
    [NonAction]
    [CapSubscribe("test/pub")]
    public void ReceiveMessage(Dictionary<string, object> data) {
        var jsonstr = JsonSerializer.Serialize(data, new JsonSerializerOptions {
            WriteIndented = true
        });
        Console.WriteLine(jsonstr);
    }
}
```
