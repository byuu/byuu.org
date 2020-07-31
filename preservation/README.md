# SNES Preservation Project

byuu spent [many years and thousands of dollars][desc]
collecting and dumping SNES and Super Famicom games.

[desc]: /about/#snes-preservation-project

![byuu's SNES game collection](/images/preservation/byuu-snes-games.jpg)

Although he did not manage to redump *every* cartridge before his retirement,
he did manage to dump most of them,
and published an in-progress database
of the results he had gathered.
Updates and extensions to this data are available
in the [higan](../higan/) and [bsnes](../bsnes/) emulators.

# Boards

Although there were thousands of commercially-released games
for the SNES and Super Famicom,
they mostly used one of a few different circuit-board designs,
which determined where the game's data would appear in the memory map,
what special chips were present and where *they* appeared, etc.

  - [Boards (Production).bml](./Boards (Production).bml)

This file is normally built into the emulator.

# Cartridges

The cartridge databases identify each cartridge by the SHA256 of its content.
Each record provides a human readable name,
the ID of the circuit board it uses,
and how the game's data fits onto that circuit board.

Note that the SHA256 includes the main ROM data
plus [concatenated firmware](../higan/firmware/),
which most widely-available ROM images do not include.

Commercial games, grouped by release region:

  - [Super Comboy (KOR).bml](./Super Comboy (KOR).bml)
  - [Super Famicom (HKG).bml](./Super Famicom (HKG).bml)
  - [Super Famicom (JPN).bml](./Super Famicom (JPN).bml)
  - [Super Famicom (ROC).bml](./Super Famicom (ROC).bml)
  - [Super Nintendo (AUS).bml](./Super Nintendo (AUS).bml)
  - [Super Nintendo (BRA).bml](./Super Nintendo (BRA).bml)
  - [Super Nintendo (CAN).bml](./Super Nintendo (CAN).bml)
  - [Super Nintendo (ESP).bml](./Super Nintendo (ESP).bml)
  - [Super Nintendo (EUR).bml](./Super Nintendo (EUR).bml)
  - [Super Nintendo (FAH).bml](./Super Nintendo (FAH).bml)
  - [Super Nintendo (FRA).bml](./Super Nintendo (FRA).bml)
  - [Super Nintendo (FRG).bml](./Super Nintendo (FRG).bml)
  - [Super Nintendo (GPS).bml](./Super Nintendo (GPS).bml)
  - [Super Nintendo (HOL).bml](./Super Nintendo (HOL).bml)
  - [Super Nintendo (ITA).bml](./Super Nintendo (ITA).bml)
  - [Super Nintendo (LTN).bml](./Super Nintendo (LTN).bml)
  - [Super Nintendo (NOE).bml](./Super Nintendo (NOE).bml)
  - [Super Nintendo (SCN).bml](./Super Nintendo (SCN).bml)
  - [Super Nintendo (UKV).bml](./Super Nintendo (UKV).bml)
  - [Super Nintendo (USA).bml](./Super Nintendo (USA).bml)

Memory packs for the [Satellaview] add-on:

  - [BS Memory (JPN).bml](./BS Memory (JPN).bml)

[Satellaview]: https://en.wikipedia.org/wiki/Satellaview

Mini-cartridges for the [Sufami Turbo]:

  - [Sufami Turbo (JPN).bml](./Sufami Turbo (JPN).bml)

[Sufami Turbo]: https://en.wikipedia.org/wiki/Sufami_Turbo

Prototypes and other limited-availability releases:

  - [Prototypes (JPN).bml](./Prototypes (JPN).bml)
