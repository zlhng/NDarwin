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

## Conventions
- Namespaces follow folders: `NDarwin.Scanning`, `NDarwin.Motion`, ... (`App/` files use `NDarwin`).
- When adding a source file, add it to `NDarwin.csproj` too.
- Usage: `NDarwin.exe [profile file or name] [--lang en|zh]`
