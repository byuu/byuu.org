![higan logo](/images/higan/logo.png)

# higan — "Now you're playing with fire!"

higan is a multi-system emulator that began development as "bsnes" on October
14th, 2004.  The purpose of higan is to serve as hardware documentation in
source code form: it is meant to be as accurate and complete as possible,
with code that is easy to read and understand.

It was originally developed by byuu,
but in March 2020 it was handed over to the community
and byuu continued development under the name [ares](/ares).
It is available under the GNU GPL version 3 or later.

  - [Source code](https://github.com/higan-emu/higan)

# Documentation

  - [Game Paks (folders)](/higan/game-paks)
  - [Firmware](/higan/firmware)
  - [User Guide (article)](/higan/user-guide)

# Screenshot

![higan Main Window](/images/higan/higan.png)

# Supported systems

higan currently emulates the following systems:

  - [Nintendo Famicom](#famicom)
  - [Nintendo Famicom Disk System](#famicom-disk-system)
  - [Nintendo Super Famicom](#super-famicom)
  - [Nintendo Super Game Boy](#super-game-boy)
  - [Nintendo Game Boy](#game-boy)
  - [Nintendo Game Boy Color](#game-boy-color)
  - [Nintendo Game Boy Advance](#game-boy-advance)
  - [Nintendo Game Boy Player](#game-boy-player)
  - [Sega SG-1000](#sg-1000)
  - [Sega SC-3000](#sg-3000)
  - [Sega Master System](#master-system)
  - [Sega Game Gear](#game-gear)
  - [Sega Mega Drive](#mega-drive)
  - [Sega Mega CD](#mega-cd)
  - [NEC PC Engine](#pc-engine)
  - [NEC SuperGrafx](#supergrafx)
  - [MSX](#msx)
  - [MSX2](#msx2)
  - [ColecoVision](#colecovision)
  - [SNK Neo Geo Pocket](#neo-geo-pocket)
  - [SNK Neo Geo Pocket Color](#neo-geo-pocket-color)
  - [Bandai WonderSwan](#wonderswan)
  - [Bandai WonderSwan Color](#wonderswan-color)
  - [Bandai SwanCrystal](#swancrystal)
  - [Benesse Pocket Challenge V2](#pocket-challenge-v2)

## Famicom

![Gimmick!](/images/higan/core-nes.png)

Famicom emulation in higan is very mature, including full support for the MMC5,
Sunsoft-5B (and its YM2149), VRC6 (and its custom sound chip), VRC7 (and
its YM2413), and many more. Even the recent VRC5 is supported.

The key weakness in the Famicom core is currently the reliance upon iNES
mappers, which lack all of the necessary information to determine how to emulate
certain games. A database will be needed to fully support all games, which at
this time I have not yet created.

Further, higan does not have support for unofficial mappers, which limits its
use with many Chinese software titles.

## Famicom Disk System

![Zelda no Densetsu](/images/higan/core-fds.png)

The Famicom Disk System is also supported, including its custom FM synthesis
sound channel. Images in higan use the raw digital format of these disks, which
include padding and checksum information. Using icarus, FDS
images stored with this information trimmed off can be imported, and the missing
data regenerated.

## Super Famicom

![Bahamut Lagoon](/images/higan/byuu-snes.png)

The Super Famicom is the most well-emulated system in higan, on account of the
entire project being an evolution upon what was originally [bsnes](/bsnes),
to which more emulators were added at later dates.

Every single component is emulated at the raw clock level, every coprocessor is
implemented using LLE (low-level emulation) techniques, and this core has
received extensive testing over the past 15+ years by thousands of players.

Currently, there are zero known bugs in higan's SNES emulation, and I work
tirelessly to ensure that continues to remain the case as often as possible.

I know of no SNES emulation more complete than this.

As a fun bit of history, I once led a project in 2011 to decap every SNES
coprocessor to extract and emulate its firmware, rather than continue relying on
the pre-existing HLE (high-level emulation) that was used in previous SNES
emulators.

## Super Game Boy

higan and bsnes are the only two true Super Game Boy emulators that fully
emulate the SNES side of the system, which is required for 100% of the available
functionality to operate correcttly.

higan's Super Game Boy emulation is powered through its own Game Boy emulation
core.

## Game Boy

![Link's Awakening](/images/higan/core-gb.png)

higan's Game Boy emulation is only roughly middle-of-the-road. The Game Boy is
deceptively one of the hardest systems to emulate accurately, considering the
myriad of subtle hardware revisions all with their own bizarre quirks and edge
cases.

That said, it's enough to run once-difficult games such as Pinball Fantasies,
and recent work has improved the emulation by a good margin, so it's not a bad
choice by any means.

## Game Boy Color

![Shin Megami Tensei - DC Black Book](/images/higan/core-gbc.png)

The Game Boy Color is also supported, along with a relatively decent simulation
of the unusual color profile of the system.

Like with the Game Boy core, more work is needed to really refine the accuracy
of this system as well.

## Game Boy Advance

![Golden Sun](/images/higan/core-gba.png)

higan is roughly tied for the most accurate timing emulation for the Game Boy
Advance, with extensive effort placed into ROM prefetch emulation, and the only
pixel-based renderer in a GBA core.

But as a result, it's also one of the more demanding cores, and it's still not
perfect.

A major factor that holds back higan's GBA emulation is the lack of a games
database for the various save types used by games. The built-in heuristics fail
on games that intentionally try to fool emulation attempts. Overriding the
heuristics manually is possible through custom manifest files, but that is far
from user-friendly or intuitive.

## Game Boy Player

higan doesn't actually emulate a full-on GameCube this time around (yet?), but
it does emulate the serial communication protocol to provide working rumble
controller emulation for games that support it, which is really the only useful
thing the Game Boy Player does. It's sadly not nearly as cool as the Super Game
Boy was in terms of adding new functionality to games.

## SG-1000

![Ninja Princess](/images/higan/core-sg1000.png)

The SG-1000 is emulated relatively well, and is very simple hardware. There's a
few edge cases that don't work yet, but nearly all games should run very well.

## SC-3000

The SC-3000 is not as well supported, as the computer-specific portions are not
really emulated. I haven't decided how far I want to go in emulating this
system, but the basics are in place at least.

## Master System

![Phantasy Star](/images/higan/core-ms.png)

The Master System is very well emulated, including full support for the YM2413
FM synthesis audio expansion used by game titles such as Phantasy Star.

## Game Gear

![Sonic the Hedgehog](/images/higan/core-gg.png)

The Game Gear is also fully supported and highly compatible.

## Mega Drive

![Sonic the Hedgehog 3](/images/higan/core-md.png)

Mega Drive emulation is in its relatively early stages.

It has extremely cycle accurate 68K and Z80 emulation, as well as very
high-quality PSG and YM2612 emulation, but the lack of VDP FIFO timing emulation
holds it back a bit from the more demanding demoscene software out there.

The audio is a particular point of pride in any case, modeling very closely to
real hardware using Artemio's MDFourier analysis software.

higan also emulated the Game Genie and Sonic & Knuckles lock-on cart. And unique
to higan, you can continually stack these cartridges as many times as you like,
forming the infamous "tower of power" -- there's even an easter egg that
emulates the effects you would see if you stacked too many cartridges together
on a real system. Try it to find out what it is!

## Mega CD

![Lunar 2: Eternal Blue](/images/higan/core-mcd.png)

If Mega Drive is in its early stages, Mega CD emulation is in its alpha stages.

Still, it's far enough along to play my favorite two video games of all time:
Lunar: The Silver Star and Lunar 2: Eternal Blue.

I ended up going down quite a rabbit hole when it comes to emulating the CD
drive for this system, aiming to support the native lead-in TOC from CDs that is
missing from formats like BIN/CUE, I provide real emulation of the Reed-Solomon
Product Codes that exist within data track sectors, and I even emulate the CD
audio pre-emphasis flag.

However, arguably the third best game on the system, Popful Mail, currently does
not boot, so there is still work to be done on this core for sure.

Fun history fact: the first time I considered getting involved in the emulation
scene was 1998, where it was my dream to be able to emulate the Mega CD, which
at the time was but a pipe dream to everyone.

It may have taken me 20 years to get there, but I did ultimately manage to
(mostly) get there!

### Help Wanted

More than with any other core, I could desperately use help in improving higan's
Mega CD emulation. Weighing in at a staggering three CPUs, two video chipsets,
and four audio chipsets, debugging issues in Mega CD emulation is a true
challenge, made worse by there being zero mature emulator debuggers for this
system with which to compare my emulation against to look for potential
problems.

If you can help, please get in touch with me via the social media contact
buttons above, thanks!

## PC Engine

![Neutopia II](/images/higan/core-pce.png)

PC Engine support is rather robust, with nearly all games being fully playable.
There are certainly edge cases that could use work here, but for general
gameplay things work quite well.

The way I emulate the video is rather complex: the PC Engine actually has the
equivalent of video monitor modelines, which let you position and stretch the
screen in various different ways. The low-level emulation of these tends to be
rather demanding, and it also results in the overscan areas being visible, which
is why in the screenshots for this system the video is not centered.

For PC Engine games, I simulate the PC Engine CD peripheral being attached, to
give each game 2KB of BRAM (backup RAM) for game saves. Each game gets its own
unique copy of BRAM, so you can save your progress in games like Neutopia and
Neutopia II without the need for passwords or save states.

## SuperGrafx

![Dai Makai Mura](/images/higan/core-sgx.png)

The SuperGrafx is also well supported with full compatibility for the entire
library of ... five software titles. Seriously.

It is however likely the most demanding core in higan on account of it taking
the already complex PC Engine graphics chip, adding a second one, and then
adding a complicated third chip to merge the two graphics chip outputs into one
onscreen result. So much engineering effort for so few games.

## PC Engine CD

PC Engine CD emulation is planned for a future release, but is currently not
supported, sorry.

## MSX

![Parodius](/images/higan/core-msx.png)

MSX emulation is far from state-of-the-art, and only cartridge-based games that
do not use mappers are currently supported.

Even with just this, it's enough to run a surprisingly large amount of software.

## MSX2

![Akumajou Dracula](/images/higan/core-msx2.png)

The MSX2 and its much more advanced graphics chipset is also supported.

## MSX2+

The MSX2+ is not supported, and there are currently no plans to support it.

## MSX turbo-R

The MSX turbo-R is not supported, and the odds of it ever being supported are
*extremely* slim, sorry.

## ColecoVision

![Frogger](/images/higan/core-cv.png)

The ColecoVision is emulated well enough. I really only added this core because
the processers used are identical to the Master System and MSX. Because hey, why
not?

## Coleco Adam

I don't have any plans to support the Coleco Adam at this time, but maybe one
day if I have absolutely nothing else to work on.

## Neo Geo Pocket

![Samurai Shodown!](/images/higan/core-ngp.png)

Neo Geo Pocket emulation has never really advanced in the entire emulation scene
much beyond the absolute basics, but I've still done my best to advance the
state of the art here, and while my compatibility may not be as high yet, I do
believe I have the most accurate emulation of the original hardware.

I spent months painstakingly going through the TMP95C061F datasheet and
emulating every last feature that was even remotely feasible (which means there
are still features that aren't ... I could write a book at how over-engineered
the SoC that powers the Neo Geo Pocket is.)

As a sign of its timing accuracy, higan is currently the only Neo Geo Pocket
emulator to play mic's YM chiptune emulator homebrew correctly.

higan supports full emulation of the system BIOS, rather than relying on HLE
(high-level emulation) techniques.

## Neo Geo Pocket Color

![The Last Blade](/images/higan/core-ngpc.png)

The Neo Geo Pocket Color is of course supported as well.

## WonderSwan

![Langrisser Millenium](/images/higan/core-ws.png)

The WonderSwan is another oft-neglected system in the emulation world, but I do
feel that higan's emulation of this system is very complete. I even optionally
display the system status icons that are found on the real WonderSwan hardware.

Screen rotation plays heavily into the WonderSwan library, and higan offers both
automatic and manual screen rotation with automatic transposing of inputs, so
that you don't have to map inputs in both portrait and landscape orientations.

Recently, I paid out a $1,000 bounty to furrtek to extract the boot ROMs from
this system so that we could emulate the startup splash screen and system
settings menu for more faithful emulation. higan is currently the only emulator
to support these boot ROMs.

## WonderSwan Color

![Riviera: The Promised Land](/images/higan/core-wsc.png)

The WonderSwan Color is also fully supported.

## SwanCrystal

The SwanCrystal is mostly just the WonderSwan Color with a better LCD panel
(though still no backlight, sadly.) However, there are a few small changes that
higan also emulates, including a slightly different boot ROM.

## Pocket Challenge V2

This was an educational system released by Benesse, but since it uses the same
underlying hardware as the WonderSwan, I went ahead and supported it for
completeness.

It bypasses the boot ROM, removes the system status icons, and changes all of
the input buttons to new meanings. The cartridge slot is also modified slightly.
