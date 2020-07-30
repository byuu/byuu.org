higan utilizes "Game Paks", or game folders, for loading games. It uses
the icarus import tool to create these gamepaks from individual game ROM files.

Gamepaks are an attempt to simulate physical Nintendo Game Paks in digital form.
The idea is that for each game, one folder acts as a gamepak, and contains all
data that is specific to said game.

Much as your save data is bound to a physical cartridge, so too is your save
data to a game folder.

# Visual Demonstration

Let's say you store all your games in the `C:\Games` directory.
If they were stored as game paks,
you would only have to configure one path:

| Game Folders | `C:\Games` |

...and you might wind up with a structure like this:

    📂 C:\Games
        📂 Super Mario Kart (NA).sfc
            📄 program.rom
            📄 save.ram
            📄 cheats.bml
            📄 uPD7725.program.rom
            📄 uPD7725.data.rom
        📂 Dai Kaijuu Monogatari II (JP).sfc
            📄 program.rom
            📄 save.ram
            📄 rtc.ram
            📄 state-1.bst

On the other hand,
if you use the traditional organization scheme most emulators use,
you have to configure five paths:

| ROM path        | `C:\Games\ROMs\`     |
| Save path       | `C:\Games\Saves\`    |
| Firmware path   | `C:\Games\Firmware\` |
| Cheat path      | `C:\Games\Cheats\`   |
| Save State path | `C:\Games\States\`   |

...and you would wind up with a structure like this:

    📂 C:\Games
        📂 ROMs
            📄 Super Mario Kart (NA).sfc
            📄 Dai Kaijuu Monogatari II (JP).sfc
        📂 Saves
            📄 Super Mario Kart (NA).srm
            📄 Dai Kaijuu Monogatari II (JP).srm
            📄 Dai Kaijuu Monogatari II (JP).rtc
        📂 Firmware
            📄 dsp1.program.rom
            📄 dsp1.data.rom
        📂 Cheats
            📄 Super Mario Kart (NA).cht
        📂 States
            📄 Dai Kaijuu Monogatari II (JP).bst

# Prelude

It's very important that everyone understand that the move from loading
individual game ROM files with path configurations for each file type over to
using folders for each individual game was not an arbitrary or capricious
change.

It was born out of *necessity* as bsnes grew beyond all other SNES emulators
that came before it, to support many new scenarios where single game ROM files
were simply no longer adequate.

I'm very much aware that many people do not like this design, and that many have
refused to even consider using higan over it. However, I hope people will at
least read through this article and try to understand my rationale.

# Motivation #1: Memory Mapping

Not all video game cartridges are the same: Nintendo cartridges contain complex
mapping hardware that can exist in many configurations. For the US SNES set
alone, there are 85 unique board configurations comprising 49 unique mapping
combinations. And there are many more board types in the Japanese SFC set.

The old notion of "LoROM" and "HiROM" only barely begin to describe things. And
indeed, emulators have long used many hacks to work around incompatibilies
caused by such over-simplification.

I started work on an SNES preservation project, where my goal was to purchase
every commercial SNES game, and analyze the full 16MB address space to produce
bit-perfect mappings. This work is now available in icarus.

Instead of "good enough" to run games through the use of hacks, bsnes' memory
mapping is *perfect* for all games that I have dumped and verified. And if
you've followed bsnes over the years, you'll know that I aim for perfection.

The information on the board layouts and memory mapping are not included with
raw game ROM dumps: it must be stored somewhere.

By creating the icarus tool, I have been able to include this mapping
information in a central database. However, I can never hope to describe every
SNES game in existence: not the least because new homebrew software continues to
be made to this day.

Further, we have stumbled across multiple examples of prototypes and tech demos
that do not have valid registration headers for heuristics to work on.

Thus, for these reasons, it was necessary to allow external files to specify
customized memory mapping for individual games.

For just two examples, this has allowed bsnes to be the only SNES emulator
capable of running both the DSP-1 tech demo ROM and neviksti's 96mbit Star Ocean
hack.

These mapping files must reside somewhere, and I have placed them inside higan
gamepaks as "manifest.bml" files.

# Motivation #2: Coprocessor Firmware

In the past, SNES emulators used a technique known as HLE (high level emulation)
to support SNES coprocessors. For example, the DSP1 coprocessor is used in games
such as Super Mario Kart and Pilotwings.

HLE is, however, a flawed and imprecise method of emulation. It relies on pure
speculation to *simulate*, rather than *emulate*, the behavior of chips.
This leads to inaccuracies, and a total lack of timing which results in software
running much faster than it really should.

Through years of hard work, funding, and help, bsnes became the first SNES
emulator to truly *emulate* SNES coprocessor firmware.

In actuality, coprocessors are actual CPUs with their own program firmware
running inside of them. This LLE (low level emulation) requires this firmware to
be made available to it.

This has allowed bsnes to be the first emulator to ever emulate games such as
SD Gundam GX and the Hayazashi Nidan Morita Shougi games.

However, this firmware is also not included with simple game ROM images. Like
the memory mapping file, it must be stored somewhere.

It gets even more complicated ... take the case of Super Mario Kart. There have
been two revisions of this game: one with the DSP1, and one with the DSP1B,
which is a bug-fix version of the original. The game ROM is 100% identical for
both versions of this cartridge. By keeping the firmware separate from the game
itself, it is not possible to allow both cartridges to be emulated.

Further, there is now the potential for homebrew to take advantage of these
coprocessors with their very own firmware, allowing potentially very exciting
future homebrew developers.

So for these reasons, firmware needs to be bundled with each game. And once
again, as with memory map manifests, I include this data inside each gamepak.

# Motivation #3: Multi-Game Carts

bsnes also became the first (and is currently the only) emulator to support the
competition cartridges: Campus Challenge '92 and Powerfest '94.

Unlike traditional games, these boards consist of three separate games, and a
master control program that selects between them.

There was a need to be able to store all four game pieces in such a way that
they could be loaded together and played.

Once again, gamepaks provided the solution: each individual game is stored
inside of one gamepak, and the entire competition cartridge can be loaded and
played as one unit.

# Interlude

That's not to say gamepaks are strictly a matter of necessity. They truly do
offer many compelling advantages over the old paradigm of separating files by
type.

# Advantage #1: Convenience Moving, Copying and Renaming

If you look at the example, gamepaks offer a clear organization advantage over
traditional game ROM file storage.

If you ever wish to copy a specific game to another location, you need only
locate the game, copy it, and paste it in another location. All data comes
along with it and is ready to go. Just like a real Nintendo Game Pak.

If you want to rename a game, you only need to change the name of one single
item and you are finished.

Whereas with the traditional method, you must go into (potentially) multiple
folders to copy each individual piece, or risk losing data. And when you want to
rename things, you must repeat yourself several times. Make one mistake, and the
data will no longer match up. And this tends to accumulate cruft as game ROMs
are removed or renamed, but stale save data remains.

# Advantage #2: Convenience Configuring the Emulator

With gamepaks, you need only (optionally) set one single path location to where
you want your games stored.

Whereas with game files sorted by type, you must either configure several
separate paths for each file type, or have everything jumbled together into one
giant mess of a single folder.

# Advantage #3: Development Convenience

Gamepaks are also very friendly to debuggers. It becomes easy to store lots of
development files right inside the gamepak: CPU instruction trace logs, memory
RAM dumps, memory usage analysis logs, source code, symbol files, etc.

This avoids having to add several additional path configuration options, or
completely flood folders with unintuitive file extensions. It also makes
cleaning up the results trivial: simply delete the Debug/ folder inside of a
gamepak, and you're good to go.

The split nature of files also aids in development: if you are working on NES
software, the program ROM (instructions) and character ROM (graphics) are
cleanly separated. You can load one into your disassembler, and the other into
your tile editor, without cross-contamination of unrelated data that would show
up as garbage.

# Advantage #4: Clear Meanings for Files; Loss of Ambiguitiy Between Systems

If you want to locate the save RAM for a game, which file name is more
intuitive? `save.ram` or `game.srm`? If you want to locate the program ROM,
which is more apparent? `game.sfc` or `program.rom`?

This has further benefits for a multi-system emulator like higan.

Traditionally, NES emulators use the .sav extension for save RAM, whereas SNES
emulators use the .srm extension. NES emulators use the .nes extension for the
program ROMs, whereas SNES emulators use the .sfc extension.

With higan, each system has a consistent naming convention: your save RAM is
always labeled `save.ram`.

# Postlude

Of course, that's not to say it's all positive. There are two issues caused by
gamepaks.

# Drawback #1: Compatibility

Although this format would be trivial for other emulators to support, it's
unlikely that many will choose to do so.

Few emulators are as in-depth as bsnes is, so there usually isn't a strong
impetus to support such flexibility.

This creates a problem when one wants to run the same game on multiple
emulators.

I've designed the icarus tool to try and ease this burden as much as possible,
but at the end of the day, you will need to keep around two copies of games if
you wish to run them in multiple emulators.

For the most part, this generally shouldn't be an issue for most. As bsnes
offers 100% compatibility with zero known bugs, there's no need to work around
bugs by switching between emulators as one used to have to do in the past.

However, this can be a source of frustration if one is using another emulator
for specific features higan lacks such as debugging, tool-assisted speedruns, or
netplay.

# Drawback #2: File Associations

Unfortunately, the most popular operating system with >90% market share lacks
the ability out of the box to support folder associations.

So by default, it's not possible to associate a gamepak with higan to open once
double-clicked.

*However*, I have created the kaijuu Windows Explorer shell extension to
alleviate this pain point entirely. After installing kaijuu, you can do many
useful things, including associating folders that end in specific extensions
like .sfc with higan.

Of course, it's still a drawback as you have to install kaijuu, as it doesn't
seem appropriate to bundle it in with higan.

# Conclusion

In reality, it's traditional retro game emulators that act highly unusual: higan
stores game data in the same way pretty much every other class of application
does.

When you install games from Steam, each game goes into its own directory.

When you download music, each song goes into a folder for each album.

When you download TV series, each episode goes into a folder for each show.

It's always been the norm for humans to sort by "item", and not by "file
extension", it's just that the very first major retro emulator was designed for
a different time and with no foresight into the nuance that would arise in the
future.

And because technology is typically dictated by "first to ship" rather than
technical superiority, we've been stuck with that bad decision ever since.
