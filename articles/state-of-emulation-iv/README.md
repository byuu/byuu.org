> This article was originally published on 2016-04-03,
> the day before higan v098 was released.
> That version was the last to include the original "balanced" profile
> (with the scanline-based PPU renderer)
> and the "performance" profile,
> leaving only the "accuracy" profile with the dot-based PPU renderer.

# The State of Emulation, Part IV

It's been nearly six years since the last article in this series. Since then, bsnes has evoled into the multi-system emulator, higan.

## Low-Level Coprocessor Emulation

Focusing on the SNES, the final major milestone was full low-level emulation of SNES coprocessors: the DSP-n series (NEC uPD7725), ST-01n series (NEC uPD96050), ST-018 (ARM v3) and Cx4 (Hitachi HG51B169). This was a huge accomplishment made possible by the work of countless individuals and the help of many donors to fundraise the costs associated with decapping these chips to extract their firmware.

Yet with the completion of this important goal, we've finally consumed all of the significant advances that remain in the realm of SNES emulation. As such, progress has really slowed down over the past four years now, because there just isn't that much to do anymore.

That's not to say there's been no progress, nor that more isn't coming, of course. But there's nothing remaining that's going to grab any headlines.

## The Advent of Gamepaks

As a consequence of DSP LLE, coprocessor firmware became a requirement to play many major SNES games.

Furthermore, I began a preservation project to collect and redump every SNES game ever released. In doing so, it became apparently clear that our emulation of the SNES memory map for games was very flawed: rather than emulate which areas of memory were unmapped (open bus), we simply mirrored ROM and RAM into every possible location in the hopes of maximizing compatibility. Along with several nasty game-specific memory mapping hacks, we were able to get this functional for all games, but a hack is a hack, and bsnes has always been about eliminating hacks, and so with my dumping project, I began mapping out the exact memory layouts of each and every game in the library. This change brought with it the requirement for cartridge mapping information.

Finally, I added support for a new feature known as MSU1: this was an artificial enhancement coprocessor designed to add up to 4GiB of storage and to allow CD-quality audio streaming. But instead of being emulator-only, it was designed to work on real hardware. And thanks to ikari's sd2snes, it now does so! However, this new support further required a very large data ROM, and music files for each CD-audio track used by MSU1.

All of these advances combined pushed the old system of storing all game ROMs in the same folder to its breaking point. The old organizational system of specifying separate paths for each file type (save RAM, save states, cheat codes, etc) no longer scaled with coprocessor firmware, cartridge mapping information, and MSU1 audio/data files added to the mix.

So this brought about game folders, or gamepaks. The idea was to have one folder for each video game, where all files for said game would be stored within said folder. Aside from years of growing pains as variations on the cartridge mapping syntax and file naming, I did eventually land on a stable and backward-compatible system for these gamepaks.

## Complexity Creep

Unfortunately, gamepaks were a major departure from the way traditional emulators worked. And indeed, no other emulators were eager to implement this new system. Not the least of which because they all lacked the new features of bsnes, and would thus have no use for them.

This change also created severe backlash amongst bsnes users; literally decimating the userbase from ~100,000 downloads a release to around ~10,000 per release. It alienated many long-time supporters, turned some into foes of the project, and resulted in roughly a dozen forks of bsnes.

This was, in a sense, a long time coming. Super Game Boy, BS-X Satellaview and Sufami Turbo emulation had already complicated game loading. Multiple peripherals had complicated input configuration. DSP LLE had greatly slowed down emulation and complicated game loading. The dot-based PPU renderer cut performance in half; which spawned a complicated system involving multiple emulation profiles that confused users. Emulating more and more of the SNES resulted in the necessity to scale back features to keep the user interface sane.

The addition of Super Game Boy support landed a Game Boy and Game Boy Color emulator in bsnes. The addition of the ST018 led to most of the work being in place, and ultimately led to bsnes gaining a Game Boy Advance emulator. A desire to round out the emulator set eventually led to a Famicom emulator, and most recently, a WonderSwan and WonderSwan Color emulator. These additional emulators further required simplifying and removing SNES-specific settings from the user interface, alienating even more users.

## higan

Ultimately, the growing number of emulated systems made the bsnes name increasingly inaccurate. A new name was needed that didn't imply the emulator being specific to just the SNES, and so the project was rebranded as higan.

While it was certainly gamepaks that caused the biggest revolt, a clear pattern had emerged: in order for bsnes/higan to grow, complexity would continue to increase, and performance would continue to suffer.

## Complexity

The complexity is just going to keep soaring.

Recently, a prototype of the Nintendo PlayStation, the failed hardware merger between Nintendo and Sony, emerged. After obtaining the BIOS, work has begun to emulate this device. While it's not all that practical with no games available for it, it is a very interesting piece of hardware, and very fun to try and preserve this hugely important piece of gaming history.

But this device is not simple: for the first time, now higan has to consider how to load and access CD-ROMs. Even worse, it has to do this not from a cartridge, but from an expansion port device. Furthermore, it should probably be allowed to eject and insert new CDs while the system is running. But higan has no mechanisms for this, and adding them will only serve to complicate the user interface more.

Famicom Disk System emulation will hopefully land at some point in the future, which will bring with it more complexities.

Both the Famicom and Super Famicom have dozens of complex peripherals that bring in all kinds of newe complexities. Take the SNES Voicer-Kun: this was a user-programmable IR blaster that would let you play vocal tracks from included audio CDs for Japanese drama games. Emulating this is going to require connecting SNES input peripherals to the audio mixing system in higan, and these games are going to then require FLAC audio rips of the CDs to be included in their relevant game folders, which will make playing these games even tougher. Especially as nobody has ever bothered to image these audio CDs before.

Or how about the Barcode Battler? The Lasabirdie golf club? The Exertainment exercise bike? How in the *hell* do you even emulate items like this?? I certainly don't know, but I do know it's going to require lots of new code, lots of new user interface extensions, and lots of configuration.

And then there's improving the Satellaview emulation: where we get to emulate a now-defunct satellite network to bring the BS-X Town back to life. And to properly emulate this system, we have to allow the Satellaview flash cartridges to be writable. And in doing this, we will restore the Satellaview's play count limits. Won't it be fun when the stock BIOS automatically erases your games because you've played them too many times?

Or how about the NTT modem? If we want to play the JRA PAT and SPAT games, we'll have to emulate a dial-up modem, and a remote ISP that was used to place real-life bets on horse racing games. I don't even think it's going to be possible to do anything useful with this. But simulating a dial-up modem through an emulated controller sure doesn't sound like fun.

## Performance

Meanwhile, my hopes that CPU performance would grow to enable bsnes to run even on low-end ARM hardware has yet to come to fruition. While ARM has *very slowly* made strides toward running faster, the x86 hasn't really picked up much speed.

The focus has shifted toward adding more and more processor cores to CPUs, and this ends up lowering their performance to mitigate added heat generation. But extra cores do not help classic emulators that require such tight synchronization that everything has to be implemented on a single CPU core.

At the moment, I can't even conceive of a time when I might be able to properly emulate the SA-1's bus conflict manager that inserts stalls into the slave CPU when the master CPU is accessing the same bus. We simply don't have fast enough CPUs for this. And it's not just me saying this, even _Demo_ from ZSNES once mentioned how it would require a ~10GHz CPU to emulate the SA-1 perfectly.

And to make matters worse, the balanced and performance cores of bsnes have really hit a dead-end. They've been nothing but an albatross that has made improvements to the primary accuracy core of bsnes more difficult, and complicated the codebase, compilation, distribution, usage, etc.

I had hoped to eventually retire them as processor speeds picked up, but that hasn't happened. Yet keeping them around hasn't gained us anything, either. By their very design of compromising accuracy for performance, they really can't be improved.

The realization is that new releases are only slowing these cores down. For instance, v097 added simulation of interlacing, scanlines and color bleed; which resulted in both a speed hit and breakage of certain pixel shaders that relied on the lower resolution these cores allowed in previous releases through a very complicated per-line width design.

## The Future

Perhaps the worst of this, is that all of the future complexity and performance penalties are going to be for hardware features and support of things that virtually nobody cares about.

Emulation is always a system of increasing costs and decreasing rewards. And as I've explained in the past, both are exponential, rather than linear.

Overall, this paints a fairly bleak picture of the future. But that's the reality of where we're at.

If my goal were simply to create the most well-loved emulator by the largest amount of people possible, I would have had to have ceased development around bsnes v073. If my goal were to create the ideal "accurate but still usable" emulator, I'd have to stop development today.

But that's a sad end. There is so much more to do ... and there always will be. The lack of popularity of something shouldn't mean that it never gets preserved. You and I may not have much interest in the Voicer-Kun, but I've had Japanese people reach out to me and ask me about it. And I do want to emulate it, as well as everything else I've talked about.

And so, going forward, my intention is to drop the balanced and performance SNES cores from higan entirely. They are a dead end representing the past. The old versions will remain available, and hopefully we can keep them in a maintenance mode as a separate project to keep them alive. But that'll be highly dependent upon my free time and energy levels, which have been steadily dropping over the past few years.

Most of the value of these cores have been eroded anyway through the countless forks of bsnes that have sought to stall bsnes at past points that were more favorable to end users by being faster and easier to use.

Thus, the future of higan looks bleak. The project is likely to become increasingly unpopular, slower, and more difficult to use in the name of progress.

I don't expect others to understand why I'd choose to go this route, nor do I expect people to stay on board and continue using higan going forward, but I do hope that at least people will respect that my ultimate goal is preservation; not making the most popular emulator.
