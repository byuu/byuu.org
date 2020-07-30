higan requires various firmware files to emulate certain games.

Firmware can represent boot ROMs, BIOS ROMs, program ROMs, and data ROMs. It can
refer to both system firmware (contained inside game system hardware) and game
firmware (contained inside components within game cartridges.)

higan only includes system firmware that is not subject to copyright law. It
does not include any game firmware, regardless of copyright status (although
nearly all of it is copyrighted.)

## System Firmware: Game Boy Advance

The Game Boy Advance requires a 16KiB BIOS ROM. Many GBA emulators will utilize
high-level emulation (HLE) to simulate the functions of the BIOS. But this in
turn sacrifices accuracy, especially timing.

With higan's primary goal being accuracy, this means it will only rely on
low-level emulation (LLE), which means the BIOS is absolutely required.

Upon attempting to load a GBA game in higan for the first time, you will receive
a dialog message informing you that the GBA BIOS is missing, and where to place
the file. Once you have done this, higan will be able to play GBA games.

## Game Firmware

Game firmware is present in components such as the SNES coprocessors (DSP-x,
Cx4, ST-01x, SGB, etc.)

When importing games, icarus will first look for firmware appended to games,
and failing that, scan the same directory of the game to locate external
firmware files. If it cannot find them, then you will receive a dialog message
informing you of the missing file and where to place it.

Only when firmware is appended to game ROMs will icarus be able to locate games
in its internal database to provide bit-perfect memory mapping. The reason for
that limitation is explained below.

# Game Distribution - Reality

As game firmware is part of game cartridges themselves, they should be included
with the game ROM images they apply to.

Unfortunately, the groups responsible for such things (eg No-Intro) do not
agree, and they split the firmware files into separate archives. This causes a
lot of pain for anyone who cares about accuracy.

But here are some facts about game firmware:

## Game firmware is small

The DSP-n firmware weighs in at 8KiB. The Cx4 firmware at 3KiB.

## Game firmware is unique

With the exception of the 8KiB DSP-1 (used in about ten games) and the 3KiB Cx4
(used in two games), all of the SNES game firmware is unique.

For instance, the ST-010 firmware is only used in F1 Race of Champions II. The
ST-011 firmware is only used in Hayazashi Nidan Morita Shougi. The ST-018
firmware is only used in Hayazashi Nidan Morita Shougi 2. The Super Game Boy
boot ROM is used only by the Super Game Boy.

This is because the actual firmware code is part of the game code itself: it
often has code that is exclusive to that specific game. Without the firmware,
the game ROM is thus incomplete.

As unique firmware only exists within a single game, there are thus no space
savings to be had by separating firmware from game ROMs.

## Game firmware is required for identification

Take the case of the DSP-1. There were two revisions to this firmware. The
original, and the DSP-1B.

SNES ROM images contain no indication of which revision of the DSP-1 to use. And
this is a real problem: Pilotwings requires the DSP-1. Without it, the plane in
the opening will crash. Ballz 3D requires the DSP-1B. Without it, the game will
lock up once a battle begins.

But it gets even worse: Super Mario Kart was released with both the DSP-1, and
later on, with the DSP-1B. But the main game ROM was not modified to reflect any
change.

The end result is that there exist two revisions of Super Mario Kart. If the
firmware is not included, then it is impossible to distinguish between these two
versions; and thus, it is impossible to preserve both revisions of this game.

## Game firmware exists in multiple formats

Very early versions of the SNES coprocessor extractions were created with
unnecessary padding bytes in the program ROM. After that, the earliest NEC uPD
firmware files were stored in big endian format.

For consistency and simplicity, the current NEC uPD firmware is stored in little
endian format with no padding bytes. Yet the old files still circulate online.

SNES coprocessors often have multiple pieces of firmware: for instance, the SNES
DSP-n and ST-018 firmware contains both a program ROM and data ROM. Sometimes,
the firmware is distributed with these two files merged into one. Other times,
it is split into separate files.

## Game firmware exists with multiple naming conventions

Merged coprocessor firmware contains names such as `dsp1.rom`

Split coprocessor firmware contains names such as `dsp1.program.rom` and
`dsp1.data.rom`

No-Intro stores the firmware as `[BIOS] DSP1 (World).zip/[BIOS] DSP1 (World).bin`

Yes, the 8KiB firmware is compressed, the name is needlessly repeated inside the
archive file, and for reasons that defy sanity — region codes are appended to
the names.

MAME ... we won't even talk about MAME. Suffice to say, they do things
differently as well.

And this is just going to continue on like this, every time someone else comes
along and decides to name things differently. It's impossible to predict all the
endless variations that will eventually result if things continue this way. And
without predictability, emulators can't utilize these files to provide better
emulation.

# Game Distribution - Ideal

Due to all of the issues mentioned above, the best course of action for storing
game ROMs for preservation is to append the firmware to the end of the primary
game ROM files into one single image file. By doing this:

 1. the game ROM image files will be 100% complete, and contain all of the code
    and data required to play them.
 2. cases such as Super Mario Kart's alternate DSP-1 revisions will be possible
    to represent and preserve.
 3. game ROMs will have exactly one checksum (hash) value. This allows the use
    of databases to identify the game information that cannot be stored
    inside ROM data; such as PCB layout and configuration, game title,
    peripherals used, etc.
 4. emulators will be freed from trying to guess what file names to locate for
    firmware.
 5. emulators will be freed from trying to guess what file format the
    firmware is stored in.
 6. emulators will be freed from looking from both merged and split firmware
    styles; both inside and outside of compressed archives.
 7. by including the firmware with the game, ROM hacks that seek to modify or
    improve firmware will be able to patch games with eg a BPS patch
    file. It's not as extreme an idea as it might sound: there have already
    been experimental ROM hacks that have utilized custom Cx4 code made.
 8. it will remain possible to compress games into ZIP archives, or merge them
    into solid archive 7zip archive sets, without interfering with how to
    process the firmware components.
 9. most importantly: emulators that care about accuracy and rely on LLE
    will no longer be at a disadvantage to emulators that don't and use HLE
    to simulate firmware instead.

The fears of doing this are overplayed:

 1. because game firmware is so small and so rare, it will not add much to game
    set sizes. It would add roughly ~100KiB onto the ~4GiB of ROM data that
    represents the SNES set compared to storing them separately. That's an
    increase of ~0.002%.
 2. compatibility will be maintained. The existing popular two SNES emulators,
    which have been discontinued for nine and five years respectively, still
    load and play games even with firmware appended. They simply ignore the
    extra data.

So for these reasons, I would strongly advocate for groups like No-Intro to
reconsider their position and move to appending game firmware to game ROM images
instead.

I would also encourage any future SNES emulator authors to adopt this format. To
that aim, higan already supports (and works best with) this merged ROM format.
