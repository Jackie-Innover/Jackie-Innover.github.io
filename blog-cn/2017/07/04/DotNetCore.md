# .Net Core

- [.Net Core是什么](#Net Core是什么)
- ​







### .Net Core是什么

.Net Core是一个通用开发平台, 由Microsoft和GitHub上的.Net社区共同维护. 它是跨平台的, 支持Windows, MacOS和Linux, 并且可用于设备, 云和嵌入式/IOT.

以下特征对.Net Core进行了最好的定义:

- **部署灵活**: Can be included in your app or installed side-by-side user- or machine-wide.可以包含在应用或已安装的并行用户或计算机范围中。
- **跨平台**: 可以在 Windows、MacOS 和 Linux 上运行；也可移植到其他操作系统。 Microsoft、其他公司和个人提供的支持的操作系统 (OS)、CPU 和应用程序方案会随着时间推移而增多。
- **命令行工具**: All product scenarios can be exercised at the command-line. 可在命令行中执行所有产品方案.
- **兼容性：** .NET Core 通过 [.NET 标准库](https://docs.microsoft.com/zh-cn/dotnet/standard/library)与 .NET Framework、Xamarin 和 Mono 兼容.
- **开源**：.NET Core 是一个开放源平台，使用 MIT 和 Apache 2 许可证。 文档由 CC-BY 许可发行。 .NET Core 是一个 .NET Foundation 项目。
- **由 Microsoft 支持：**.NET Core 由 Microsoft 依据 [.NET Core Support](https://www.microsoft.com/net/core/support/)提供支持



.Net Core包括以下部分:

- **.Net runtime**: 提供类型系统、程序集加载、垃圾回收器、本机互操作和其他基本服务。
- **框架库**: 提供基元数据类型、应用编写类型和基本实用程序。
- **SDK工具和语言编译器**: 提供基本的开发人员体验, available in the [.NET Core SDK](https://docs.microsoft.com/en-us/dotnet/core/sdk).
- **The 'dotnet' app host**, which is used to launch .NET Core apps. It selects the runtime and hosts the runtime, provides an assembly loading policy and launches the app. The same host is also used to launch SDK tools in much the same way.



**The .Net Core Recipe**

- **CoreFX**: .Net Core Framework
- **CoreCLI**: Command Line Interface
- **CoreCLR**: Common Language Runtime
- **CoreRT**: Native Runtime



> CoreFx goals:
>
> - Abstract the platform
> - Authentically .Net
> - Open Source
> - Support **NSL**



> **NSL**: .Net Standard Library
>
> PCL: Portable Class Library



> CLI goals
>
> - Getting started files
> - Native & IL compile
> - Restore dependencies
> - Publish app packages
> - Create NuGet packs



> CLR
>
> - Abstract the platform
> - Ensure environment
> - Manage resources



> CoreRT
>
> The embedded runtime that ships with your app.
>
> - Leverage .Net Native
>   - Native C# compilation with the standard C++ Optimizer.
> - Provide a runtime
> - Provide GC



Key Commands:

- dotnet new
  - Creates minimal files
  - Project types
    - Console
    - Web
    - Library
    - MSTest
    - XUnitTest
- dotnet restore
  - Restore dependencies
  - Create local cache
- dotnet build
  - Builds project
    - Does not invoke restore
  - Backed by MSBuild
- dotnet run
  - Invokes build
  - Executes project
  - Hosts the process
- dotnet publish
  - Build as Debug | Release
    - See dotnet msbuild
  - Generate package
    - Framework-dependent app
    - Self-contained (w/runtime)
  - Target platform
    - <RuntimeIdentifier/> (RID)
- dotnet pack
  - Creates nuspec
  - Creates nupkg

>Pack creates a NuGet package.
>
>Push prepares an app bundle.

Welcome back to csproj

- Wildcard items
- Nuget references
- Multiple frameworks
- No more GUID project - types

