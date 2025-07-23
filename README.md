# Into the Breach Vita

<p align="center"><img src="./screenshots/game.png"></p>

This is a wrapper/port of <b>Into the Breach</b> for the *PS Vita*.

The port works by loading the official Android ARMv7 executables in memory, resolving their imports with native functions and patching it in order to properly run.
By doing so, it's basically as if we emulate a minimalist Android environment in which we run natively the executables as they are.

## Notes

- Due to the nature of the executable, it is impossible to re-implement proper Netflix subscription check. Please do download and use this loader only if you own an active Netflix subscription.
- The loader has been tested with v.1.2.92 of the game.

## Controls
The Android game lacks controller support but the code for it is fully in the executable, so i restored it and enabled in the Vita loader (including cool PS4 icons). L and R triggers are mapped to L2/R2 and the back touch is mapped to L1/R1. Touch controls are still usable.

## Changelog

### v1.0

- Initial Release.

## Setup Instructions (For End Users)

- Install [kubridge](https://github.com/TheOfficialFloW/kubridge/releases/) and [FdFix](https://github.com/TheOfficialFloW/FdFix/releases/) by copying `kubridge.skprx` and `fd_fix.skprx` to your taiHEN plugins folder (usually `ux0:tai`) and adding two entries to your `config.txt` under `*KERNEL`:
  
```
  *KERNEL
  ux0:tai/kubridge.skprx
  ux0:tai/fd_fix.skprx
```

**Note** Don't install fd_fix.skprx if you're using rePatch plugin

- **Optional**: Install [PSVshell](https://github.com/Electry/PSVshell/releases) to overclock your device to 500Mhz.
- Install `libshacccg.suprx`, if you don't have it already, by following [this guide](https://samilops2.gitbook.io/vita-troubleshooting-guide/shader-compiler/extract-libshacccg.suprx).
- Extract `libfmodstudio.suprx` from PCSE01188 or PCSE01426 following [this guide](https://gist.github.com/hatoving/99253e1b3efdefeaf0ca66e0c5dc7089).
- Install the vpk from Release tab.
- Obtain your copy of *Into the Breach* legally for Android in form of an `.apk` file.
- Open the apk with your zip explorer and extract the files `libmain.so` and `libfreetype2.so` from the `lib/armeabi-v7a` folder to `ux0:data/breach`. 
- Extract all the files inside the `assets` folder in `ux0:data/breach`.

## Build Instructions (For Developers)

In order to build the loader, you'll need a [vitasdk](https://github.com/vitasdk) build fully compiled with softfp usage.  
You can find a precompiled version here: https://github.com/vitasdk/buildscripts/actions/runs/1102643776.  
Additionally, you'll need these libraries to be compiled as well with `-mfloat-abi=softfp` added to their CFLAGS:

- [SDL2_vitagl](https://github.com/Northfear/SDL/tree/vitagl)

- [libmathneon](https://github.com/Rinnegatamante/math-neon)

  - ```bash
    make install
    ```

- [vitaShaRK](https://github.com/Rinnegatamante/vitaShaRK)

  - ```bash
    make install
    ```

- [kubridge](https://github.com/TheOfficialFloW/kubridge)

  - ```bash
    mkdir build && cd build
    cmake .. && make install
    ```

- [vitaGL](https://github.com/Rinnegatamante/vitaGL)

  - ````bash
    make SOFTFP_ABI=1 HAVE_GLSL_SUPPORT=1 CIRCULAR_VERTEX_POOL=2 NO_DEBUG=1 install
    ````

After all these requirements are met, you can compile the loader with the following commands:

```bash
mkdir build && cd build
cmake .. && make
```

## Credits

- TheFloW for the original .so loader.
- Wans for the Livearea assets.
- CatoTheYounger for the screenshots and for testing the homebrew.
- Northfear for the SDL2 fork with vitaGL as backend.
