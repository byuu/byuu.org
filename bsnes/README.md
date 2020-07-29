![bsnes logo](/images/bsnes/logo.png)

bsnes is a Super Nintendo / Super Famicom emulator that began development on
October 14th, 2004. It focuses on performance, features, and ease of use.

It was originally developed by byuu,
but since his retirement in March 2020,
it is now maintained by the community.
It is available under the GNU GPL version 3 or later.

  - [Official releases](https://github.com/bsnes-emu/bsnes/releases),
    including Windows binaries
  - [Source code](https://github.com/bsnes-emu/bsnes)

## Unique Features

* True Super Game Boy emulation (using the SameBoy core by Lior Halphon)
* HD mode 7 graphics (by DerKoun) with optional supersampling
* Low-level emulation of all SNES coprocessors (DSP-#, ST-01#, Cx4)
* Multi-threaded PPU graphics renderer from [csnes](https://www.reddit.com/r/emulation/comments/8zz5ip/byuu_i_wrote_a_new_snes_emulator_from_scratch/)
* Speed mode settings which retain smooth audio output (50%, 75%, 100%, 150%, 200%)
* Built-in games database with thousands of game entries
* Built-in cheat code database for hundreds of popular games (by mightymo)
* Built-in save state manager with screenshot previews and naming capabilities
* Customizable per-byte game mappings to support any cartridges, including prototype games
* 7-zip decompression support
* Extensive Satellaview emulation, including BS Memory flash write and wear-leveling emulation
* Optional higan gamepak support (standard game image files are also fully supported!)
* Advanced mapping system allowing multiple bindings to every emulated input

## Standard Features

* MSU1 support
* BPS and IPS soft-patching support
* Save states with undo and redo support (for reverting accidental saves and loads)
* OpenGL multi-pass pixel shaders
* Several built-in software filters, including HQ2x (by MaxSt) and snes_ntsc (by blargg)
* Adaptive sync and dynamic rate control for perfect audio/video synchronization
* Just-in-time input polling for minimal input latency
* Run-ahead support for removing internal game engine input latency
* Support for Direct3D exclusive mode video
* Support for WASAPI exclusive mode low-latency audio
* Periodic auto-saving of game saves
* Auto-saving of states when unloading games, and auto-resuming of states when reloading games
* Sprite limit disable support
* Cubic audio interpolation support
* Optional high-level emulation of most SNES coprocessors
* Optional emulation of flaws in older emulators for compatibility with older unofficial software
* CPU, SA1, and SuperFX overclocking support
* Frame advance support
* Screenshot support
* Cheat code search support
* Movie recording and playback support
* Rewind support
* HiDPI support
* Multi-monitor support
* Turbo support for controller inputs

# Preview

![Bahamut Lagoon](/images/bsnes/byuu-bsnes-bahamutlagoon.png)

![Chrono Trigger](/images/bsnes/byuu-bsnes-chronotrigger.png)

![Tales of Phantasia](/images/bsnes/byuu-bsnes-tales.png)

![Metal Combat](/images/bsnes/byuu-bsnes-metalcombat.png)

![The Legend of Zelda: A Link to the Past](/images/bsnes/byuu-bsnes-zelda3.png)

bsnes boasts 100% bug-free compatibility, ensuring that every game just works
out of the box.

![Starfox](/images/bsnes/byuu-bsnes-starfox.png)

![Super Mario World 2: Yoshi's Island](/images/bsnes/byuu-bsnes-yoshisisland.png)

![Kirby's Dream Land 3](/images/bsnes/byuu-bsnes-kirby3.png)

bsnes has full low-level support for even the most complex SNES coprocessors
like the SuperFX and SA-1.

![Star Ocean](/images/bsnes/byuu-bsnes-starocean.png)

![Tengai Makyou Zero](/images/bsnes/byuu-bsnes-tengaimakyou.png)

Decompression chips and real-time clocks are also fully emulated.

![Super Mario Kart](/images/bsnes/byuu-bsnes-mariokart.png)

![F1 Race of Champions II](/images/bsnes/byuu-bsnes-f1roc2.png)

![Rockman X2](/images/bsnes/byuu-bsnes-rockmanx2.png)

![Hayazashi Nidan Morita Shougi 2](/images/bsnes/byuu-bsnes-shougi2.png)

Every digital signal processor has full low-level emulation support.

![Super Game Boy + Pokemon Yellow](/images/bsnes/byuu-bsnes-sgb.png)

Even the Super Game Boy is fully supported, as are the Satellaview and Sufami
Turbo.

# Interface

![Software Filters](/images/bsnes/byuu-bsnes-ui-filters.png)

All of the popular software filters are present.

![Pixel Shaders](/images/bsnes/byuu-bsnes-ui-shaders.png)

In addition, many OpenGL pixel shaders are included out of the box.

![Movie Recording](/images/bsnes/byuu-bsnes-ui-movies.png)

Many tools are included such as movie recording, screenshot captures, speed
adjustments, a cheat code editor, cheat code searching, and much more.

![Emulation Enhancements](/images/bsnes/byuu-bsnes-ui-enhancements.png)

bsnes supports many game enhancements, such as run-ahead, overclocking,
deinterlacing, sprite limit removal, enhanced audio output, and more.

![Driver Settings](/images/bsnes/byuu-bsnes-ui-drivers.png)

Dozens of drivers are provided so that bsnes can be configured optimally for any
setup. Adaptive sync and dynamic rate control are both supported.

![Save State Manager](/images/bsnes/byuu-bsnes-ui-statemanager.png)

An advanced save state manager lets you categorize and name your save states.
