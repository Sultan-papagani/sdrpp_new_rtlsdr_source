# sdrpp_new_rtlsdr_source
### a new rtl-sdr source for sdr++ with librtlsdr/librtlsdr and it implements the r820/t2 tuner hack and manual controls.

# Caution !
### Only works on rtl-sdr with r820 / r820t2 tuners. Using it with a wrong tuner may destroy your device because of the register hack

#Building for Windows:

## 1) Add the "new_rtl_sdr_source" folder to "SDRPlusPlus/source_modules"

## 2) On SDRPlusPlus/CMakeLists.txt:
```
32 option(OPT_BUILD_NEW_RTL_SDR_SOURCE "Build RTL-SDR Source Module (Dependencies: librtlsdr)" ON)
.
.
194 if (OPT_BUILD_NEW_RTL_SDR_SOURCE)
195 add_subdirectory("source_modules/new_rtl_sdr_source")
196 endif (OPT_BUILD_NEW_RTL_SDR_SOURCE)
```

## 3) Windows build looks for "C:\Program Files\PothosSDR\include" folder to find the librtlsdr header files. changed those header files with this repos header
```
https://github.com/librtlsdr/librtlsdr
and the files you are gonna change are;
rtl-tcp.h
rtl-sdr.h
rtl-sdr_export.h
```

## 4) And finally when you build the sdr++ you are gonna need the rtlsdr.dll BECAUSE sdr++ uses the prebuild ones on the PothosSdr which will not work. so build the librtlsdr.dll from;
```
https://github.com/librtlsdr/librtlsdr
```
## 5) i used mingw64 to compile because msvc wont work idk why aaand rename the built file: "librtlsdr.dll" to "rtlsdr.dll" and put it on "SDRPlusPlus\build\Release" folder or wherever the sdrpp.exe is.

## 6) enjoy. 

#### also if you open the project on vscode probably all the lines will be red because vscode cant find the rtlsdr files but it compiles fine.


