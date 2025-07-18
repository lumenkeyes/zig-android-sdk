# SDL2 Example

This is a copy-paste of [Andrew Kelly's SDL Zig Demo](https://github.com/andrewrk/sdl-zig-demo) but running on Android. The build is setup so you can also target your native operating system as well.

### Build and run natively on your operating system or install/run on Android device

```sh
zig build run           # Native
zig build run -Dandroid # Android
```

### Build, install to test one target against a local emulator and run

```sh
zig build -Dtarget=x86_64-linux-android
adb install ./zig-out/bin/sdl-zig-demo.apk
adb shell am start -S -W -n com.zig.sdl2/com.zig.sdl2.ZigSDLActivity
```

### Build and install for all supported Android targets

```sh
zig build -Dandroid=true
adb install ./zig-out/bin/sdl-zig-demo.apk
```

### Uninstall your application

If installing your application fails with something like:
```
adb: failed to install ./zig-out/bin/sdl2.apk: Failure [INSTALL_FAILED_UPDATE_INCOMPATIBLE: Existing package com.zig.sdl2 signatures do not match newer version; ignoring!]
```

```sh
adb uninstall "com.zig.sdl2"
```

### View logs of application

Powershell (app doesn't need to be running)
```sh
adb logcat | Select-String com.zig.sdl2:
```

Bash (app doesn't need running to be running)
```sh
adb logcat com.zig.sdl2:D *:S
```

Bash (app must be running, logs everything by the process including modules)
```sh
adb logcat --pid=`adb shell pidof -s com.zig.sdl2`
```
