> This article was originally published on 2004-10-12,
> a few days before work began on bsnes.
> The original title was *Emulation: Hardware or Software?*,
> but since *The State of Emulation, Part II* is clearly a direct sequel,
> it's been renamed *The State of Emulation* for clarity.
> 
> Also, there were supposed to be images,
> but they have been lost.

# The State of Emulation

Ask any author what their motivation is for writing an emulator. Likely, they’ll tell you it’s to preserve old hardware that will one day wear out or become unobtainable, or for development purposes like creation of homebrew ROMs.

But is this really the case? I propose it’s not.

Early work on my Tekkaman Blade hack shown on a real SNES. Obviously corrupt.

My experience in console programming has been on the Super Nintendo (SNES). I began coding in 1997, which means I’ve been programming for it longer than most programmers did back when it was still getting new games.

ZSNES, the most prominent SNES emulator, emulates 99 percent of commercial ROMs. Even with such a high compatibility rate, it fails to simulate even the most basic attributes of the system.

A real SNES does not let programmers write to Video RAM (VRAM) while the screen redraws. Emulators don’t seem to mind at all. A real SNES will not allow you to set the tile priority bit on a graphic layer if only one layer is in use. Again, emulators don’t seem to mind. This results in scrambled looking images on the screen of the real SNES.

Even the controller support has yet to be emulated properly. The SNES has two ways of checking to see what buttons are pressed, a process called “polling.” In ZSNES and Snes9x, both of these methods are flawed.

Dual Orb 2 translation by Nightcrawler running on a real SNES. Yes/No options remain Japanese.

When you poll using the manual method, you get 1 bit from the register 12 times. The other 7 bits returned are of an undefined state. When most emulators poll, they return the top 7 bits as always clear. If you don’t set these 7 bits to zero before checking the status of the joypad, your program may end up thinking a button was pressed when it was not.

The automatic method relies on the SNES to poll the joypad for you. However, it tends to report that buttons are not pressed down, even if the button is held down. It causes something similar to a turbo effect. The result is ZSNES and the SNES perform very different.

Imagine a platform game where you hold right after pressing B to jump over a pit. Now imagine if halfway over the pit, the game assumed you let go of the right direction. Into the pit you go.

Gideon Zhi's translation of Ys IV: Mask of the Sun, running on an actual SNES. No text ever displays.

Another frustrating problem is how all current SNES emulators handle the JSL command (Jump to Subroutine Long), a code to hop from one area of a program to another.

On an actual SNES, if this is the first code in your program and it switches banks, the program will die and cease to play after returning from the routine. It will only work after you press the reset button. This affects a significant number of the splash screens shown at the start of translations and old ROM releases.

While it may seem like I’m picking on ZSNES, I’m not. All emulators have these problems to some degree, and all of these problems are interrelated. It’s unrealistic to use an emulator for development or testing. Even Super Sleuth, an emulator “designed to aid in development” has these problems.

No matter which emulator you pick, some code functions very differently on a real system. Something every ROM hacker to touch assembler has discovered.

RPGOne's Dragon Quest I title screen on an actual SNES. The English in the flame fails to display.

Grab a copy of Gideon Zhi’s translation of Ys IV: Mask of the Sun and see for yourself. On a real SNES, absolutely no text is visible. Gideon’s hack attempts to write to Video RAM while the screen is still drawing the graphics. Yet ZSNES will happily play it, as if nothing at all is wrong.

Still not convinced? Pick up the most recent patch for Dragon Quest I & II Reprise by RPGOne. You’ll notice that in emulators, the game’s title in the flames is in English. But on the SNES, it’s still in Japanese.

Look at Dual Orb II, translated by Nightcrawler. In an emulator, the “Yes / No” options look completely normal. Try the same ROM on an actual SNES and watch as the boxes are now magically in Japanese.

Sometimes these limitations come in handy, however. Dark Force, of DeJap Translations, for example, decided to release two patches for Bahamut Lagoon: one that plays on only actual hardware and one that plays only in emulators. The emulator specific patch takes advantage of things that are not possible on a real SNES in order to run certain scenes faster. But does this really represent emulation?

How Star Ocean should look when the S-DD1 chip is gone.

Even if every game you throw at your emulator of choice plays perfectly, it’s still not properly emulating a real SNES. The authors claim to be emulating the hardware, but they’re not. They may be extremely capable of running commercial ROM images, but none behave like a true SNES with all its limitations.

It might be that commercial games never issue such bad commands, since professional developers already knew they wouldn’t work on a SNES. Is the lack of bad commands in commercial games the reason limitations have never been emulated?

If this is true, it means the goal of emulation is not to duplicate how the system performs, but simply to emulate as little hardware as needed to run commercial ROMs.

This isn’t a new problem. Look at the numerous patches that fail to work on real hardware, or the various posts about these issues on emulator message boards. While it is quite probable that many of these issues are presently unknown to emulation authors, several of them have been brought up before in the past, and remain uncorrected. There only seem to be two or three individuals who even care about this and raise the issues publicly.

Enix's Star Ocean as it appears in ZSNES without graphic packs to fake lack of S-DD1 emulation.

One person, Neviksti, has devoted a lot of time to exact comparison of emulator and SNES performance. Unfortunately, he isn’t the official author of any SNES emulators.

A few years ago, some people dumped compressed graphics from all the SNES titles with unemulated chips, and then released the copyrighted graphics as a pack to make the games playable in ZSNES. That’s how Star Ocean, Street Fighter Alpha 2 and Far East of Eden Zero became playable without ever emulating the S-DD1 or SPC7110.

There’s no question this is a great achievement for anyone hoping to play these games, but it’s utterly useless if emulating the SNES, and even more useless if a homebrewer wanted to take advantage of these technologies in a new game. MAME has already chosen to remove support for games that ran by methods other than true emulation.

While there has been some progress into emulating the SPC7110, it is still ethically questionable from an emulation standpoint as to whether it should be supported by graphics packs as it is presently.

The S-DD1 was successfully reverse-engineered by a gentleman named Andreas Naive — no affiliation to any emulator. His method was published August 17, 2003. One year later, the main ZSNES build still does not include S-DD1 emulation. Snes9x excelled in this area, as they implemented this even before Andreas made his work public. The first version of Snes9x to include S-DD1 emulation was 1.42, released December 4, 2003.

In early Der Langrisser hack work, VBLANK issues caused character names to fail to appear correctly.

So if emulators don’t emulate the limitations needed to be a development platform and do not strive to emulate original hardware, what are they trying to achieve besides running as many commercial games as possible?

As a side note, it is worth mentioning the hard work going into SNEeSe. Its author, Charles Bilyue, is trying to emulate the SNES and its limitations. Sadly, it’s not yet full-featured enough to be an attractive platform. Even SNEeSe allows execution of some code that does not work on real hardware.

“Well then byuu, why don’t you fix the problems?”

It’s not my job. I program for the SNES, I do not program SNES emulators. Even with all my work, it’s certain I’ve only scratched the surface of a vast sea of problems caused by failing to emulate the system’s limitations. If we truly want to preserve the SNES for all time, we need to make sure that we understand it completely first.

My goal is not to shoot down the work of emulation authors on all systems over the years, they have done amazing work. It’s that this work doesn’t coincide with what authors claim emulation is all about, and the lack of any attempt at faithful emulation is also hindering progress in translations and homebrews.

Even though without emulators, there may have never even been a translation scene, a true attempt at hardware emulation is long overdue.

For comparison pictures showing both actual hardware and emulators, check the Related Images link below.

## Retractions

- The Bahamut Lagoon emulator-specific patch was intended as a speedup, not a workaround.
- The S-DD1 and the SPC7110 both decompress graphics, not decrypt them. The SPC7110 also has other functions.
- According to Nach, Andreas worked with the Snes9x developers to get it into the private build before he released his findings. It was not released months after.
