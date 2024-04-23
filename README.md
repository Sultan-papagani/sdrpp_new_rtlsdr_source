# sdrpp_new_rtlsdr_source

## Hey heeey! there is even newer&better rtl-sdr source, check it out [here](https://github.com/Sultan-papagani/sdrpp_rtlsdr_source)

New rtl-sdr source for sdr++ which implements manual controls for r820/r820t2/r828d tuners.

![photo1](https://github.com/Sultan-papagani/sdrpp_new_rtlsdr_source/assets/69393574/920c01d4-c3fa-40b9-a60a-2151a50fd69e)
![photo2](https://github.com/Sultan-papagani/sdrpp_new_rtlsdr_source/assets/69393574/5373c07d-df57-48a4-b941-39b844962c43)

## Features
* Harmonic reception (allows reception up to 6GHz)
* Dithering
* 3 Stage gain control
* 4 Filter controls

## Needed Hardware
* rtl-sdr with a r820/r820t2/r828d tuner (yes rtl-sdr v4 also supported)

# Installing

## Windows

Download prebuilt .dll files from Release
* Replace the rtlsdr.dll with the new one
* Put "new_rtl_sdr_source.dll" into "modules" folder
* Launch sdrpp.exe and add the new module from "Module Manager"
* Go to "Source" and select "NEW-RTL-SDR"

## Other

There are currently no existing packages for other distributions

# Building on Windows

1) Add the "new_rtl_sdr_source" folder to "SDRPlusPlus/source_modules"

2) On SDRPlusPlus/CMakeLists.txt add:
```
32 option(OPT_BUILD_NEW_RTL_SDR_SOURCE "Build RTL-SDR Source Module (Dependencies: librtlsdr)" ON)
.
194 if (OPT_BUILD_NEW_RTL_SDR_SOURCE)
195 add_subdirectory("source_modules/new_rtl_sdr_source")
196 endif (OPT_BUILD_NEW_RTL_SDR_SOURCE)
```

3) Windows build looks for "C:\Program Files\PothosSDR\include" folder to find the librtlsdr header files. change those header files with this repos header
```
https://github.com/librtlsdr/librtlsdr
and the files you are gonna change are;
rtl-tcp.h
rtl-sdr.h
rtl-sdr_export.h
```

4) And finally when you build the sdr++ you are gonna need the rtlsdr.dll because sdr++ uses the prebuilt ones on the PothosSdr which will not work. so build the librtlsdr.dll from;
```
https://github.com/librtlsdr/librtlsdr
(i used mingw64 to compile because of msvc erros)
```

5) Rename the built file: "librtlsdr.dll" to "rtlsdr.dll" and put it on "SDRPlusPlus\build\Release" folder or wherever the sdrpp.exe is.

6) Build the project
```
cmake --build . --config Release
```

7) After building, on the "SDRPlusPlus\root_dev\config.json" files add this line to modules:[];
```
"./build/source_modules/new_rtl_sdr_source/Release/new_rtl_sdr_source.dll"
(also if you accidentally put "," on the last string, sdr++ resets all the config.json so be careful)
```

8) Launch sdr++ from the top directory
```
.\build\Release\sdrpp.exe -r root_dev -c
```

#### Windows development notice
If you open the project on vscode probably all the lines will be red because vscode cant find the rtlsdr files but it compiles fine.


# Building on Other distributions

The process should be more or less the same as in Windows. Make sure librtlsdr is from the same source.
