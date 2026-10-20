# EAStdC

[![Build Status](https://travis-ci.org/electronicarts/EAStdC.svg?branch=master)](https://travis-ci.org/electronicarts/EAStdC)

EAStdC is a package which implements a number of basic library facilities that are similar to those in the standard C library.


## Documentation

Please see [Introduction](doc/EAStdC.html).


## Narrow strings are UTF-8

EAStdC treats `char` strings as UTF-8. Its conversions between `char` and `char16_t`, `char32_t` or `wchar_t` encode and decode UTF-8, and its `char8_t` overloads copy the bytes unchanged. Text in another code page, such as Windows-1252, Windows-1251 or Shift-JIS, is not converted: it is rejected as malformed UTF-8 or produces the wrong characters.

On Windows, narrow text coming from the system, such as the `argv` of `main` and the results of the `A` versions of Win32 functions, uses the process's active code page, which by default is the system's legacy code page. Applications that use EAStdC should therefore make UTF-8 their active code page in the application manifest. This is supported from Windows 10 version 1903; older versions ignore the setting.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1">
  <application>
    <windowsSettings>
      <activeCodePage xmlns="http://schemas.microsoft.com/SMI/2019/WindowsSettings">UTF-8</activeCodePage>
    </windowsSettings>
  </application>
</assembly>
```

With CMake and MSVC, listing the `.manifest` file among an executable's sources embeds it. Also compile with `/utf-8` so that narrow string literals are encoded as UTF-8. Console output still depends on the console's own code page; see `SetConsoleOutputCP(CP_UTF8)`.


## Compiling sources

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details on compiling and testing the source.


## Credits

Roberto Parolin is the current EAStdC owner within EA and is responsible for the open source repository.


## License

Modified BSD License (3-Clause BSD license) see the file LICENSE in the project root.

