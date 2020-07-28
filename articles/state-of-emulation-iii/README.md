> This article was originally published on 2010-08-01,
> the same day that bsnes v066 was released.
> This was after a few months' work on the dot-based PPU renderer,
> and after byuu used that research to remove [the last global hack][oamhack]
> from the original scanline-based PPU renderer.

[oamhack]: /articles/state-of-emulation-ii#ppuhackoam_address_invalidation-and-ppuhackcgram_address_invalidation

# The State of Emulation, Part III

Another three years have passed. How has SNES emulation advanced? The executive summary is: very well.

## S-CPU

The S-CPU core is in fantastic shape. The most important change over the last three years was support for the hardware ALU multiplication and division delays. When an SNES program tries to multiply or divide, it must wait on the hardware to perform the operation, which takes several iterations to complete. Attempting to read the results early will return pre-computed results.

Obviously, these results are not at all useful; and we know of no commercial game that relies on this. However, this has always been a thorn in the side of SNES programmers using emulators who were not aware of this delay. Now one can be certain that if ALU code runs on bsnes, it will also run on real hardware. Developers will see any errors immediately.

Another interesting improvement has been in IRQs, which gives a great example of just how far we have to go to continue improving emulation at this point. When an IRQ executes on the most simplistic opcodes that consist of: operand fetch, I/O cycles; the second I/O cycle will be converted to a bus read. If you are executing out of a SlowROM region, this will result in a two-clock-cycle penalty. IRQs typically trigger once a frame, or very rarely as many as 262 times per frame. In the worst case, this is a timing difference of only 0.001219894%. Nonetheless, two weeks were spent writing extremely difficult edge case tests to track down exactly what was happening, and to ensure exactly which opcodes would trigger this edge case, as well as whether or not the actual read occurs (it does.)

Lastly, there was the case of Speedy Gonzales. In level 6-1, there is a switch that needs to be hit to finish the level. Up until recently, this game would lock up any emulator when it was hit. You can probably imagine why this was overlooked, but it's quite a big deal to play a game that long and instantly lose all of your progress due to an emulation bug. In this case, it actually turns out to be a bug in the game itself. But as it works on hardware, it needs to work under emulation as well. It is reading from an unmapped memory address, and will not break out of this loop until it gets the value it wants. As it turns out, after so many tests, eventually the read will happen immediately after an HDMA transfer, which will update the S-CPU's memory data register, giving the game the value it needs to break out of the loop.

The one feature that is lacking from the S-CPU still is auto joypad polling. Right now, the polling happens immediately. But on real hardware, the S-CPU silently polls the joypads in the background throughout the span of three scanlines. The exact behavior turns out to be extremely complex, shifting the exact starting point after every scanline, and it exhibits all kinds of strange behaviors when you access the joypad ports during this polling process.

## S-SMP

Work is going well here, too. blargg put a lot of research into the S-SMP TEST register. We now have six of the eight bits 100% perfectly emulated, even down to the ability of certain frequency settings to permanently deadlock the processor due to bus conflicts with the S-DSP sharing the APURAM.

The last two bits affect timer operation, and we have two of those four modes emulated. This part is extremely tricky, because the exact effects vary between each SNES revision.

Outside of this, the S-SMP is considered to be virtually 100% perfect.

## S-DSP

blargg's S-DSP core is known to be 100% bit-perfect to real hardware, with the one exception that the mute command is instant, and does not exhibit a very fast fade-out effect.

Overall, it is an outstanding implementation, featuring extreme accuracy with a minimal amount of complexity and size.

## S-PPU

Perhaps the biggest improvement over the past three years has occurred in the S-PPU module.

First up, the exact behavior that Uniracers relies on to accomplish its OAM HBlank writes has been uncovered. This rules out the first of the three global hacks mentioned in the previous State of Emulation article: ppu.hack.address_invalidation.

And much more importantly, the biggest change of all—bsnes now has a dot-based S-PPU renderer. That is to say, rather than rendering entire scanlines at a fixed point, typically in the middle of the scanline, each pixel is now rendered in real-time.

As it turns out, this makes the overall emulation roughly 40% slower. This is much better than the 200-300% slower I initially predicted; and it was due to years of careful planning and consideration, which lead to the ability to run the two cores out-of-order, synchronizing only when absolutely necessary.

This rules out the other two remaining global hacks, ppu.hack.render_scanline_position and ppu.hack.obj_cache.

The effects are immediately apparent. Daikaijuu Monogatari II was a game that would disable a BG layer a little past the start of a scanline, where there was nothing on the scanline drawn yet. Failure to support this would result in the battle stats having a duplicated line. Goodbye, Antrhox is an example in the opposite direction: it disables the rest of the line too late, and it ends up drawing a single line of gibberish, static graphics on the left-most edge of the screen. It showed up on real hardware, and now it shows up under emulation.

Perhaps most importantly, this ended up having a major impact on one particular game: Air Strike Patrol. It turns out there *was* an SNES game that actually used mid-scanline raster effects. This game uses specially timed IRQs that adjust the display brightness register for a very short burst for a few scanlines in a row. The end result? True translucency on the SNES to create a shadow for your plane.

I love this example so much. It's a perfect example of a behavior that nobody ever noticed before: emulators simply couldn't handle the mid-scanline writes and would draw the entire scanline in uniform brightness. To the untrained eye, the game appeared to play perfectly fine. The casual observer could easily conclude that the emulation was flawless, when in fact it was not. But now that we know the shadow is there, actually playing the game in bsnes reveals something truly amazing: the shadow gives you a visual indication of where your planes' bombs will drop, thus making the game substantially easier to play! Imagine that.

Sometimes, the things I emulate are such extreme edge cases that we all expect they will have no effect on any commercially released games; and could be seen by some as pointless speed hits. And then you run across an example like this, and it just vindicates everything I do here.

The new dot-based renderer is still far from perfect, of course. The real S-PPU tends to cache variables throughout the rendering process; whereas the renderer in bsnes does not cache nearly enough. The net effect is that register changes may propagate to the screen a few pixels sooner in some cases. This part is going to be very hard to perfect, but the good news is that the task is now substantially easier with a working dot-based renderer: rather than requiring a massive rewrite, only minor tweaks will be needed to perfect the S-PPU once and for all.

## Special Chips

bsnes now supports every special chip that has ever been emulated. It has the best emulation out there for every chip, with the lowest-level synchronization, and the most complete implementations. The SuperFX and SA-1 are great examples of this. Games simply do not use 100% of the hardware available to them, especially for the SA-1. Up until bsnes, these features were simply left unemulated. I have filled the void and support 100% of the functionality of both coprocessors.

The SPC7110 decompression algorithm has finally been cracked by neviksti, and full support has been added to bsnes. I've always been adamantly opposed to such cop-out simulations as graphics packs, and refused to support them. It was my strong belief that by adding graphics pack to an emulator, you strip away the motivation and reward to ever actually emulate the hardware itself. Even though I was not ultimately responsible for figuring out the algorithm, I still stand by that sentiment, and I am proud to say that unlike more popular emulators, I have never succumbed to the easy way out of adding graphics packs, or game-specific hacks.

bsnes has also become the first, and currently only, SNES emulator to emulate the Super Game Boy hardware. With a huge thanks to sinamas for his Game Boy emulator, gambatte. Unlike standalone Game Boy emulators that simulate the Super Game Boy, bsnes does it right with actual emulation. This gives you things that no Game Boy emulator can claim: Donkey Kong and Contra get special sound effects, graphical borders in Castlevania are animated, and Space Invaders can upload an entire SNES game to run natively at 256x224! Along with all of the fun you've come to expect: SNES multitap support, custom SGB pack-in borders, even the ability to draw directly onto the screen using an SNES mouse. It's all there, just as you remember it.

bsnes now also has support for special custom hardware. One example is a serial port controller interface, that allows bsnes to simulate a serial port connection with a PC program. This allows bidirectional communication within the emulator. Thanks to blargg, this exists on real hardware, and such a cable can be made for only a few dollars with some simple EE skills. Another example is MSU1, which allows for full-motion video and CD-quality audio playback, and it also provides a full 4GB of accessible storage. This is meant to enhance existing games, and has already been used to add the Chrono Trigger PSX anime intro to the SNES port. It is being used by ROM hackers including myself to add amazing new soundtracks to existing titles, and it can even be used for entirely new software. And best of all, ikari_01 is hard at work at creating an actual SNES flash cartridge that supports the MSU1. So this is not just an emulation toy, it's more of a prototype of something to come for real.

## Memory Mapping

bsnes can now optionally map any game ROM any way you like, from an XML memory map file. This signals the death-knell for the made up "HiROM" and "LoROM" generic memory maps. Along with the help of many others, we are in the process now of verifying the exact memory map layouts of all cartridges. Header-based heuristics and magic bytes will soon be a relic of the past. Real hardware never looks at game headers, they can be entirely blank and still run just fine. Emulators should work the same way, and the XML memory map specification will allow exactly that.

## User Interface and Features

The GUI has been rewritten in Qt, allowing for full portability to all of the major desktop operating systems. This also allowed an amazing debugger to be added, leaving all previous SNES debuggers in the dust with its full-featuredness and first-ever features like forward and backward disassembly, read-write-execute breakpoints on any memory for any chip, graphical memory viewers, statistical summaries of all register settings and usage-based analysis of memory.

Save states are now present. Again, many years were needed for the planning, but I have managed to implement full save state support, and even rewind support, even under Super Game Boy emulation. A substantial challenge given the multi-threaded nature of the core, but a huge accomplishment, further proving that libco/cooperative-multithreading can be a great fit for all emulators, not just for the Super NES.

Mednafen has added the bsnes core for its SNES emulation, which allows for netplay support. OpenEmu has also added a bsnes core, allowing for amazing processing effects under OS X. And the core itself now has a simplistic, 12-function C interface, which can be compiled as a DLL, libsnes. This allows ports such as Richard Bannisters', to quickly and easily use bsnes, without having to target a constantly changing core. It can even be used from other languages now. This has been used by myself and others to produce GUI ports to SDL, Microsoft.NET/C#, Cocoa/Objective-C and GTK+/Python. Although the ports are largely based around experimentation, it is hoped that one day they can be used to offer highly tuned GUIs made specifically for and integrated with the most popular desktop environments. Lastly, as an April Fools' joke this year, bsnes was successfully ported to the Nintendo DS. But you don't want it, trust me ;)

I've also added blargg's File_Extractor library, and fixed up Nach's libjma to work on 64-bit targets. bsnes can now extract and run games compressed using ZIP, RAR, JMA, GZip, BZip2 and 7-zip. Even better, it supports solid and other archives containing more than one game. You are now presented with a loader menu to select which game inside the archive you want. There is also support for both UPS and IPS soft-patching.

The video renderer has gained all of the popular scalers now: nearest-neighbor, scanline, Scale2x, LQ2x, HQ2x, 2xSaI, Super 2xSaI, NTSC. Also included is pixel shader support both for Direct3D and OpenGL.

Best of all is that none of these features have bloated the core at all. Using an external DLL, any unwanted functionality can be removed simply by deleting the corresponding DLL. All very zen-like and minimalist, the GUI dynamically updates to remove all traces of the missing features.

## Licensing

Perhaps best of all, bsnes is now licensed under the GPL2, making it free software in both senses of the word.

## In Closing

The past three years have been amazing. I know that SNES emulation can never be 100% perfect, but I finally feel that I have reached a point where I could walk away from bsnes and feel that my job is done. That the SNES hardware is very well preserved for future generations.

Seeing that I can now get 45fps even on the lowest-end Intel Atom netbook processors, and over 200fps on top-of-the-line Intel Core processors, is a very encouraging sign as well. Within the next decade, I believe it will be possible to run bsnes even on handheld and portable hardware, such as cell phones.

Who knows what the future will hold. Until next time, everyone!
