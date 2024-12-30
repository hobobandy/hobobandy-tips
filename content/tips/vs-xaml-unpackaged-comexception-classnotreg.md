+++
date = '2024-12-30T14:35:27-05:00'
draft = false
title = 'Visual Studio XAML COMException CLASSNOTREG'
+++
Building an unpackaged blank WinUI 3 project, the following exception is thrown:

> System.Runtime.InteropServices.COMException: 'Class not registered (0x80040154 (REGDB_E_CLASSNOTREG))'

To fix this, add the following in the in the project's `.csproj`:

```XML
<PropertyGroup>
...
<WindowsPackageType>None</WindowsPackageType>
...
</PropertyGroup>
```
