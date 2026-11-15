# NDarwin

C# (.NET Framework, x64) console tool for industrial machine PC commissioning, forked from
`zlhng/ConsoleApp1` (DeviceScanner). Renamed: solution/project/assembly `ConsoleApp1` -> `NDarwin`,
root namespace `DeviceScanner` -> `NDarwin`.

## Layout
- `NDarwin.slnx` — solution (build `x64`)
- `NDarwin/NDarwin.csproj` — old-style csproj; every `.cs` file must be listed in a `<Compile Include>`
- `NDarwin/App/` — entry point (`Program.cs`), admin restart, firewall, scan config
- `NDarwin/Scanning/` — COM/IP device discovery, probes, address fixers, profile verification
- `NDarwin/Motion/`, `NDarwin/Native/` — ZMotion ZMC controller (ZAux P/Invoke): init, homing, discrete IO
- `NDarwin/WindowsSpec/` — Windows spec checks/fixes (OS, locale, NIC, Defender, VC runtime, drivers)
- `NDarwin/Profiles/` — `*.profile` machine profiles (copied to output) and loader
- `NDarwin/Reporting/` — run report, scan summary, PDF report
- `NDarwin/External/` — vendor DLLs referenced by HintPath; `NDarwin/Drivers/` — drivers.zip, VC redist

## Build
- Prerequisites: Visual Studio with the ".NET desktop development" workload and the
  .NET Framework 4.7.2 targeting pack (no .NET SDK needed; `dotnet build` does not apply).
- NuGet packages come from `NDarwin/packages.config` and restore into `packages\` (not in git).
  Restore once before the first build:
  `MSBuild.exe NDarwin.slnx -t:Restore -p:RestorePackagesConfig=true -p:Platform=x64 -p:Configuration=Debug`
- Build: `MSBuild.exe NDarwin.slnx -p:Platform=x64 -p:Configuration=Debug -v:minimal -nologo`
- MSBuild is not on PATH; find it with
  `"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vswhere.exe" -latest -find MSBuild\**\Bin\amd64\MSBuild.exe`
- Output: `NDarwin\bin\x64\Debug\NDarwin.exe`

## Conventions
- Namespaces follow folders: `NDarwin.Scanning`, `NDarwin.Motion`, ... (`App/` files use `NDarwin`).
- When adding a source file, add it to `NDarwin.csproj` too.
- Usage: `NDarwin.exe [profile file or name] [--lang en|zh]`
