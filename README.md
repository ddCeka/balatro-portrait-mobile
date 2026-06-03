# Balatro Portrait Mobile

A portrait mode mod for Balatro on Android - optimized for mobile gaming.

## Features

- **Portrait Mode** — Fully optimized vertical layout for mobile
- **Touch Controls** — Responsive touchscreen support with anti-jitter
- **Redesigned HUD** — Score, buttons, and panels repositioned for portrait
- **Full Game Support** — All Balatro features work in portrait mode
- **Mod Support** — Optional [Lovely](https://github.com/ethangreen-dev/lovely-injector) integration for loading mods on Android

## Requirements

- **Balatro** - You must own a legal copy of the game
- **Python 3.6+** - For build scripts
- **Openjdk-17/Openjdk-21** - For compiling apk
- **Android device** - Android 5.0+ recommended

> Works on Termux.

## Quick Start

### Step 1: Clone the Repository

```
git clone https://github.com/ddCeka/balatro-portrait-mobile.git
cd balatro-portrait-mobile
```

### Step 2: Get Balatro

**You must own a legal copy of Balatro.**

1. Purchase from [Steam](https://store.steampowered.com/app/2379780/Balatro/)
2. Find your Balatro.exe location:
   - **Steam**: Right-click Balatro → Manage → Browse Local Files
   - Default: `C:\Program Files\Steam\steamapps\common\Balatro\Balatro.exe`

### Step 3: Run the Auto Builder

```
python build.py
```


*(Your configuration will be saved in `.buildconfig.json` for rapid, single-click rebuilds later)*

| Option | Default | Description |
|--------|---------|-------------|
| CRT patch | off | Applies the CRT-disabling portrait patch. The default 2.0 build keeps this off. |
| Readabletro | on | Applies the [Readabletro](https://github.com/bladeSk/readabletro) mod: nunito font, high-res card and UI textures. |
| Lovely mod support | off | Embeds the [Lovely](https://github.com/ethangreen-dev/lovely-injector) runtime so mods can be loaded. Requires a rooted device. |

You can also pass flags to skip the prompts:

```
python build.py --no-crt --readabletro --no-lovely
python build.py --balatro "D:\Steam\steamapps\common\Balatro\Balatro.exe" --force
python build.py --balatro "~/Library/Application Support/Steam/steamapps/common/Balatro/Balatro.app" --force
```

Run `python build.py --help` or check the top of `build.py` for all available flags.

### Step 4: Install on Android

Transfer the generated APK to your phone and install it.

Or natively deploy via ADB if your device is plugged in:

```
adb install build/balatro-aligned-debugSigned.apk
```

## Project Structure

```
balatro-portrait-mobile/
├── build/                  # Contain artifacts and tools needed
├── src/                    # Modified source files (portrait mode)
├── game_original_files/    # Extracted game files (created by build.py)
├── patches/                # Custom patch for better readability
├── docs/
│   └── changelog.txt       # Contain some info of what is changed
│   └── MODDING.md          # Mod installation guide
│   └── README.md           # This file you read
│   └── requirements.txt    # Needed dependencies
└── build.py                # Build script (setup + Game.love + APK)
```

## Mod Support (Lovely)

Balatro Portrait Mobile supports the [Lovely](https://github.com/ethangreen-dev/lovely-injector) mod framework for loading mods on Android.

> **Root Required**: Installing mods requires a **rooted Android device** (e.g. via [Magisk](https://github.com/topjohnwu/Magisk)). The mod directory is located in the root filesystem (`/data/user/0/`), which is not accessible without root.

Build with `--with-lovely` (or answer "yes" during the build prompt) to embed the Lovely runtime. After installation:

1. Launch the game once to create the folder structure
2. Install [Material Files](https://play.google.com/store/apps/details?id=me.zhanghai.android.files)
3. Navigate to: `/data/user/0/com.balatro.android/files/save/ASET/Mods/`
4. Place your mod folders there and restart the game

See [docs/MODDING.md](docs/MODDING.md) for detailed instructions and troubleshooting.

## Troubleshooting

### "Game won't start"

- Make sure setup.py completed successfully
- Check that `src/resources/` and `src/localization/` exist

### "Build fails"

- Ensure Python 3.6+ is installed: `python --version`
- JDK installation is needed in environment and make sure `JAVA_HOME` are set.

### "Black ellipse covering part of the screen"

This is caused by the CRT shader not rendering correctly in portrait mode on some devices.

**Solution**: Rebuild with CRT patch enabled:

```
python build.py --crt
```

Or answer **yes** to "Apply CRT patch?" during the interactive build.

## Credits

- **LocalThunk** - Original Balatro game
- **LÖVE** - 2D game framework
- **Contributors** - Portrait mode modifications
- **KtourzaJeremy** - Some huge pull requests
- **[ethangreen-dev](https://github.com/ethangreen-dev)** - Lovely injector
- **[WilsontheWolf](https://github.com/WilsontheWolf)** - Lovely Mobile Maker & lmm-love-android
- **[bladeSk](https://github.com/bladeSk)** - Readabletro mod (fonts, shaders, textures)

## Disclaimer

This is an unofficial mod. You must own a legal copy of Balatro to use this.
The original game files are NOT included in this repository.

## License

This mod is provided as-is for personal use. All rights to Balatro belong to LocalThunk.
