> This article was written by byuu/Near in March 2020,
> before his first attempt at retirement,
> recording his story in his own words.

![byuu's long-term avatar image](/images/about/giulio.png)

I am byuu, a C++ programmer with over twenty years of experience. I'm mostly
known as an emulator developer with a focus on accuracy and games preservation.

# Inspiration

As a teenager, like many others I learned of the existence of Final Fantasy V,
the lost game not localized and released in the west that sat between the two
games we received, Final Fantasy II (IV) and Final Fantasy III (VI).

Seeing advertisements offering to import the game, I eventually saved up and
secured a copy of the Japanese release, not knowing a single word of Japanese at
that time. I figured, how hard could it be to learn some of the language?
(spoiler alert: I'm still learning.)

Shortly thereafter, I would finally make my debut on the internet under the name
of Shadow. It did not take long to locate the fan translation group RPGe that
was working to translate the game into English, which was led by a person
(Derrick Sobodash) who was using the exact same name ... awkward! But what's
more, their fan translation could be played on one's computer using emulators!

Needless to say, it felt like an entire world opened up before me, and I knew
right away that I had to be a part of that.

# Aimless Wandering

I initially approached RPGe, led by Shadow, to see if I could help in the effort
to translate Final Fantasy V, but of course not knowing any Japanese and not
having any programming experience, I was less than useful.

I then found a small group that was willing to have me, and began manually
inserting dialogue into Final Fantasy IV hard-type for Silicon Travelers. The
effort fizzled out before getting too far along.

Not to be deterred, I went out alone creating a group named Enix Translations,
hoping to tackle the unlocalized Dragon Quest games for the Super Famicom,
starting with Dragon Quest I & II.

This game really showed me the futility of trying to fan translate an entire
role-playing game using only a hex editor and no backups. Eventually after
several months of effort, the poor foundation led to the project failing as
well.

Plus at the time, others seemed to be making more progress on the Final Fantasy
and Dragon Quest games. I knew I needed to get serious, and find an original
project to call my own.

# Bahamut Lagoon

![Bahamut Lagoon](/images/higan/byuu-snes.png)

While scouring for interesting games, it was by almost sheer coincidence that I
stumbled across Bahamut Lagoon. Even though emulators of the time could not
support the color blending effects used extensively throughout the game, the
visuals, music and gameplay were truly amazing to me, and I was quickly hooked.
It was the first simulation game I'd played, and the seamless blend with
traditional RPG elements gave it a familiarity that without which I may have
been scared away from the genre.

# Starsoft

And so in 1998, I started a new fan translation group which I named Starsoft,
with the sole goal of creating a fan translation for Bahamut Lagoon.

I began self-learning how to program, with the hopes of one day creating the
tooling needed to produce a complete fan translation.

There was still the unfortunate issue of sharing a pseudonym with the founder of
RPGe, and so I also needed a new name.

# byuu

Never being particularly original with names, Bahamut Lagoon's protagonist was
the original inspiration for my name, byuu.

Today, my name holds a very different meaning for me, it is Japanese for
"(to) make a mistake": a humbling reminder to myself that perfection is not
possible, yet we can always better ourselves through the lessons we learn from
our mistakes.

![The Japanese character for byuu](/images/about/byuu-kanji.jpg)

As an aside, I would learn later that the "Byuu" from Bahamut Lagoon was simply
a bit of a pun, with the name being more appropriately translated as "View", as
in, the player "viewing" the game. So aside from others making the same
'mistake' as me (pun intended), it turned out to be an original name after all!

# Inexperience

![Bahamut Lagoon fan translation by byuu's Starsoft (menus)](/images/about/byuu-starsoft-1.png)

Even though our small team had a lot of heart, we couldn't make up for a lack of
programming experience. Still, we managed to localize many menus in the game,
and eventually we attracted the interest of Louis Bontes, the author of a
popular and fast tile editor named Naga.

Louis showed us the first glimpse of what assembly programming could do for fan
translations, by creating a bypass for the Lempel-Ziv-compressed dialogue text
in the game, and for the first time, we were able to translate the game's
prologue sequence.

![Bahamut Lagoon fan translation by byuu's Starsoft (dialogue)](/images/about/byuu-starsoft-2.png)

Unfortunately, that alone wasn't enough, and Starsoft disbanded. I kept working
on the game on my own. Inspired by Louis, I began self-teaching myself how to
program in assembler, so that I could reprogram the game as needed.

# Even More Inexperience

As incredible as emulation back then was, there was still no Sega CD emulator,
which meant my favorite games of all time, the Lunar series, were unplayable on
PCs.

I stumbled across an effort to produce a Sega CD emulator from a fellow who went
by the name of Atani. He was looking for help, and so I tried to lend a hand,
thinking that I could work on the GUI and potentially learn more along the way.

Needless to say, my hubris of the time knew no bounds, and our project went
nowhere.

# kammedo

With Starsoft dormant, a new ROM hacker by the name of kammedo emerged to work
on Bahamut Lagoon. This person was rather skilled with SNES assembly hacking,
and by this point, so was I. We got along well and quickly joined forces to try
once again at localizing this game.

This time, I had the skill to write software to extract and re-insert the
compressed dialogue text, and kammedo and I took things even further by
implementing proportional fonts throughout the game engine.

But with neither of us speaking much Japanese, we needed help. We then attracted
Tomato (Clyde Mandelin) to assist us with this.

Unfortunately, I was 16 at the time, and rather opinionated when it came to how
Japanese dialogue should be localized, and we didn't really work well together.
I take the blame in full for this, but it ultimately doomed our effort.

# Dragon Quest V

Dragon Quest is a game I fell in love with at the age of 5. Yes, 5. I even
watched the 13 episodes of the Abel Yuusha no Densetsu anime that were localized
for the west, before even knowing what anime was.

I had played through Dragon Quest I - IV as a kid, and seeing the only fan
translation for Dragon Quest V apparently dormant. I initially wanted to work
with the other group fan translating the game, but by that point my reputation
with Bahamut Lagoon preceeded me, and that wasn't allowed to happen.

Given the project claimed to be stalled due to technical challenges, and not to
be deterred, I decided to set out on my own to tackle the game. After all of my
early failures, I desperately needed my first win.

By some luck, I found spSpiff, a translator interested in taking on the game as
well. And so I pretty much worked ten hours a day, seven days a week, and in two
months' time I had the game reprogrammed to play in English. The third month was
spent polishing the code and completing the translation.

And finally, in November of 2001, I had my first completed fan translation.

![Dragon Quest V fan translation by byuu and spSpiff](/images/about/byuu-spspiff-dragon-quest-v.png)

... and so did the other group, at exactly the same time. It was such an
unfortunate and completely unnecessary duplication of effort that could have
been avoided. But nonetheless, it greatly honed my programming abilities, and I
became more humble in working with others, so overall I consider it a win.

# StarSNES

At this point, my tooling included an SNES CPU core emulator, and so I decided
to see how difficult it would be to create an SNES emulator.

I didn't get very far beyond running a few homebrew demos before giving up, and
sadly pretty much every detail about it has been lost to time now.

# Der Langrisser

Back in 1998 when I was researching games to try and work on, a second game had
also caught my eye, Der Langrisser. This one was a pure simulation game, and
thanks to Bahamut Lagoon, I was familiar with the idea and took very quickly to
it as well. It would have likely become the project I worked on, and you all
might have known me as Erwin (Der Langrisser's protagonist), if not for the fan
translation group Warui Toransu (led by alamone) that was attempting to work on
the game then.

By the time Dragon Quest V was completed, it was clear that Warui Toransu would
not be successful despite their best attempts.

By a bit of fate, it came to my attention that Derrick Sobodash of RPGe fame was
working on the game over at Clouds of El Sallia, which was something of a
precursor of a Wiki and a message board in one.

It was a good fit, and we began working together to localize this game. It ended
up taking several years to complete. Derrick instilled in me importance of
quality and polish: anything and everything we could do to enhance the
translation, I did. To the point of re-enabling and fixing the disabled
debugging mode in the game, to adding new game options to control the
translucent window background colors for better text legibility, to manually
resizing every text window to be an exact fit to our hand-drawn and hand-kerned
fonts, to fixing bugs in the original game itself.

![Der Langrisser fan translation by byuu and D](/images/about/byuu-d-der-langrisser.png)

With the help of a whole team of translators, Der Langrisser became my second
completed fan translation.

# Dai Kaijuu Monogatari

While working on Der Langrisser, I also worked on Dai Kaijuu Monogatari. At this
point, the programming work was trivial, but the game was a very tough sell and
I was never able to find a translator up for the challenge. I eventually ended
up releasing all of my tools and notes for the game and letting it go.

![My work on Dai Kaijuu Monogatari](/images/about/byuu-daikaijuu-monogatari.png)

You can see the inspiration from Bahamut Lagoon and Der Langrisser here, where I
was insistent on programming in proportional fonts for all of the menus.

# Tekkaman Blade

But there was one interesting development from Dai Kaijuu Monogatari: I needed
hand-drawn icons for the menus to replace the kanji (Japanese characters), and
Derrick offered to draw these for me in return for me reprogramming Tekkaman
Blade.

The game looked very simple, and so I agreed to what was probably the worst
trade in my life. The game ended up being a bit of a nightmare and took a good
2-3 weeks of nonstop work, but it did eventually become my third completed fan
translation.

# bsnes

Somewhere nearing the end of the Der Langrisser and Tekkaman Blade fan
translations, Derrick managed to acquire an SNES copier, allowing my work to be
tested on real hardware, and well, it didn't go well.

The emulators of the time did not really emulate the hardware limitations of the
SNES, nor did they want to, as they knew it would break many fan translations
that became dependent upon said inaccuracies. This led to me writing an article
about it, [The State of Emulation](/articles/state-of-emulation/).

Surprisingly, my venting was taken very well by the respective emulator
developers, and I decided to give writing an emulator my first really serious
attempt.

And with this, on October 14th, 2004, [the bsnes project](/bsnes)
was born.

![Tengai Makyou Zero running in bsnes](/images/bsnes/byuu-bsnes-tengaimakyou.png)

# Mother 3

By this point, Clyde and I had made amends, and he reached out to me for help in
his new fan translation attempt for Mother 3.

To that aim, I built an ARM7 cross-assembler for the reprogramming work, and
implemented a proof-of-concept dialogue patch to store the script in 8-bits per
character instead of 16-bits per character to save ROM space.

![Mother 3 fan translation](/images/about/mother-3.png)

[The project was ultimately a huge success](https://en.wikipedia.org/wiki/Mother_3_fan_translation)!
I wish I could say I had a bigger role in it, but Clyde and the others ended up
pulling most of the weight here in the end ^-^;

# Odds and Ends

Aside from the four major projects above, I worked behind the scenes (in smaller
roles) on many other successful SNES fan translations, including:

* Dragon Quest I & II
* Dragon Quest III
* Dual Orb II
* Far East of Eden: Tengai Makyou Zero
* Magical Drop
* Shin Megami Tensei II
* Shin Megami Tensei If

I also taught several prominent SNES programmers the ropes of assembly.

Furthermore, I did ultimately go back and complete all of the game reprogramming
work for my Bahamut Lagoon fan translation:

![Bahamut Lagoon 2008 by byuu (dialogue)](/images/about/byuu-bahamut-lagoon-1.png)

![Bahamut Lagoon 2008 by byuu (menus)](/images/about/byuu-bahamut-lagoon-2.png)

In fact, I did so three times to date. It's a project I come back to every
couple of years. Maybe one day I'll actually go further and insert the script so
I can produce a working patch.

# SNES Decapping Project

bsnes continued to grow and I was eventually closing in on 100% compatibility,
but limitations in the high-level emulation of SNES coprocessors was preventing
that.

A person by the pseudonym of Dr. Decapitator appeared, offering to help decap
and extract required program firmware from these coprocessors for the MAME
project. I spoke with him and coordinated a deal where he would take on the ten
coprocessors for the SNES in exchange for $250 per chip to cover parts.

This is work that traditionally costs tens of thousands of dollars per chip, so
to say it was the deal of a lifetime is quite the understatement. I pitched in
$250 myself and then fundraised the rest.

![Decapped DSP-1B coprocessor](/images/about/decap-dsp1b.jpg)

He was wildly successful with eight of them, Jonas Quinn discovered the ninth
had its program code hiding in plain sight inside the regular game ROM, and I
was able to extract the tenth and final firmware myself using my SNES-to-PC
serial cable setup.

From that point and working with many individuals such as Talarubi, segher,
Overload, Jonas Quinn and more, I was able to emulate all of these coprocessors
in bsnes, which eventually raised its compatibility to 100%!

# higan

One of the coprocessors was the ST018, which turned out to be an ARM6 core. Thus
I had most of the CPU code required to emulate the Game Boy Advance. I also had
emulated the Game Boy for the sake of Super Game Boy support, and the NES just
plainly for fun because I liked the system.

bsnes was growing and the name no longer made sense for a multi-system emulator,
and so I once again pulled from SNES JRPG protagonists, and chose Tengai Makyou
Zero's Higan for a new name for the project.

And with that, bsnes became [higan](/higan).

![Riviera running in higan](/images/higan/core-wsc.png)

# Professor Stephen Hawking

Something rather amazing came out of the SNES decapping project, and is probably
the singular most surreal moment of my life.

It would turn out that the same NEC uPD7725 processor architecture used in Super
Mario Kart and Pilotwings was also used in the SpeechProse text-to-speech module
used by none other than the late professor Stephen Hawking.

This SpeechProse hardware was bulky and fragile: it was slowly failing due to
age, and the company that made it had been long out of business.

His assistants Jonathan Wood and Peter Benie set out to emulate the machine in
software, where they became limited by the NEC uPD7720 processor it used.

They ended up reaching out to me, and with some custom modifications, they were
able to use code from higan to complete the rest of their SpeechProse emulator.

This emulator ended up being used by Stephen Hawking for the remaining 1-2 years
of his life, and was then passed on to his estate. For what it's worth, I do not
have a copy of it, and never asked for one.

For those interested, more information about this fascinating story can be found
at [The San Francisco Chronicle](https://www.sfchronicle.com/bayarea/article/The-Silicon-Valley-quest-to-preserve-Stephen-12759775.php)
or on [Peter Benie's website](http://www.chiark.greenend.org.uk/~peterb/hawking/).

# MSU1 (Media Streaming Unit)

Speaking of SNES coprocessors, we missed out on the fabled
[SNES CD-ROM add-on](https://en.wikipedia.org/wiki/Super_NES_CD-ROM), due to
disagreements between Nintendo and its partners.

Being such a huge fan of the Lunar games, I wanted to see what the SNES would be
like with such functionality, so I invented my own coprocessor, the MSU1, or
Media Streaming Unit 1.

![MSU1 logo by BMF54123](/images/about/msu1-logo.png)

Since we're long past the '90s, I saw no reason not to make it a bit better than
would have been possible at time time, and I gave it the ability to access up to
4GB of storage at transfer speeds of approximately an 18X CD-ROM drive, in
addition to the ability of being able to play Redbook CD-quality audio.

It was still important to me that it be possible on a real SNES, and I imposed
many strict limitations on myself to that effect. This proved fortuitious, when
ikari_01 later implemented MSU1 support into his SNES flash cartridge, allowing
MSU1 to be run on real SNES hardware.

I didn't really expect the idea to gain any traction, and for a few years it sat
relatively dormant until a small collection of developers really took a shine to
it and began creating patches for existing games to give them enhanced
soundtracks and sometimes even full-motion video sequences from later remakes of
said games. A person by the pseudonym of d4s even ported the Laserdisc game
Road Blaster to the SNES MSU1!

As of today, there are literally
[hundreds of MSU1 patches available](http://www.zeldix.net/f71-msu-1-hacks-database)!

Some highlights include:

* [Chrono Trigger](https://www.youtube.com/watch?v=v7U5hJCcTNI)
* [The Legend of Zelda: A Link to the Past](https://www.youtube.com/watch?v=8AKSoDFUSKA)
* [Super Metroid](https://www.youtube.com/watch?v=EdTka_nlyD8)
* [Super Road Blaster](https://www.youtube.com/watch?v=7YuWwoeAxCk)

Pretty much every major game is covered. Though certainly not for everyone, it's
proven to be a fun way of adding some replay value to classic games.

# SNES Preservation Project

With my SNES emulation having successfully reached 100% accuracy, I moved on to
trying to better preserve the SNES games library and to document the
[hundreds of various PCBs](/preservation/) used in
SNES game cartridges.

This led to my most ambitious goal yet: to buy every single SNES game ever
released in every region. A task that to this date has set me back by over
$30,000 of my own money.

I successfully completed the ~725-game North American collection, scanning and
documenting every single game and revision for it.

I was then able to fund much of the Japanese game collection through the
[rather famous eBay auction](https://www.polygon.com/2012/12/10/3749792/a-collector-is-selling-every-super-nintendo-game-for-24999)
where [I sold off my complete North American SNES collection](https://gizmodo.com/you-can-buy-every-single-snes-game-ever-for-25-000-5967342).
That was fun.

Thus I successfully purchased the ~1,450-game Japanese collection, which is to
this date still a work in progress, with the most expensive 100 titles already
completed, and the rest in queue.

And thanks to kind folks lending me their European games, I've completed around
~300 of the ~550 cartridges for this region as well.

Overall I've made substantial progress on this goal, and my
[Patreon donors](https://patreon.com/byuu) have really helped me out substantially.

# Lost European SNES Games

There was a very unfortunate incident in late-2016 where a package containing
100 PAL games valued at around $10,000 was lost in the mail due to damage during
shipping. After several agonizing months of waiting and trying everything
possible to escalate the case privately, I had no choice but to take the matter
to the public.

It generated far more press than even I had anticipated, which successfully
caught the eye of a manager at the USPS Consumer Affairs department. His team
helped locate the missing package in the Atlanta Recovery Center, where it was
slated to be auctioned off as undeliverable mail in the near future.

Thankfully, the games were recovered. I was able to preserve all of them, and
then return the games successfully to their original owner.

We learned a valuable lesson, and I no longer accept any donations unless they
are 100% fully insured. I also have a strict limit of 50 games at one time so as
to further minimize any potential losses.

# bsnes Revival

Over time, higan grew to emulate more and more systems. Every system added came
with more subtle edge-cases that needed to be emulated (be it the WonderSwan's
screen rotation support, or the Game Gear's blurry refresh rates, or the Game
Boy's rumble cartridges, and so on.) The emulator had become very difficult to
use, and the strict goal on accuracy was really taking a toll on performance.

![Current higan user interface](/images/about/byuu-higan.png)

The market also seemed to be leaning more and more toward power efficiency over
raw performance, and so I decided to bring back the old bsnes project, this time
as a standalone emulator focusing exclusively on the SNES.

Being a hard fork of higan meant that I could eat my cake and have it too: higan
could remain my personal accuracy obsession, and bsnes could gain creature
comforts that many emulator users enjoy, along with moving from a more
self-documenting code style, to one optimized for performance instead.

Today, bsnes is more than five times faster than higan, and boasts some really
impressive, one-of-a-kind features.

![higan running Lunar 2: Eternal Blue](/images/higan/core-mcd.png)

On the bright side, I did finally manage to emulate the Sega CD, 20 years
later ^-^;

# Japan

With a solid career in the real world as a software engineer, plus my
accomplishments online as byuu, I was finally able to fulfill a childhood dream
of mine and obtain a Japanese engineering visa, and I ended up moving to Tokyo,
Japan last year for work.

It's been an incredibly exciting journey so far, and even in just one year, I've
learned more Japanese than I ever had back home. I'm still far from fluent, but
it's rather amazing to be able to hold real conversations with people now.

![Tokyo, Japan](/images/about/japan.jpg)

# SNES Parallel Rendering and HD Mode 7

The main key to bsnes' enhanced performance was an idea I had to parallelize the
SNES video chipset to take advantage of the now-ubiquitous multi-core CPUs on
the market.

The results were decently impressive, but even I was very surprised at what
would come to be from this: having access to the entire video frame before
beginning rendering, a pre-requisite for parallel rendering, meant that the
affine texture mapping (rotation and zoom) effects, known colloquially as Mode
7, could be rendered at much greater detail. Given the SNES' output resolution
of 256x224, and the underlying mode 7 texture size of 1024x1024, suddenly an
extreme amount of detail could be shown onscreen without any modifications,
pixel scaling algorithms, or any other trickery being used.

This is what a programmer by the name of DerKoun implemented into bsnes, and
[the results were breathtaking](https://arstechnica.com/gaming/2019/04/hd-emulation-mod-makes-mode-7-snes-games-look-like-new/).

I eagerly merged HD mode 7 into bsnes upstream.

![HD Mode 7 in bsnes](/images/about/hd-mode-7.jpg)

# byuu.net

Given my successes with teaching SNES assembly programming, I wanted to do the
same for emulation development, and so I launched [byuu.net](https://byuu.net) as a
website dedicated to documenting and explaining the more difficult portions of
creating emulation software.

![byuu.net icon](/gallery/unscaled:icons/byuu-dot-net.png)

# Business Formation

After handling multiple licensing arrangements as an individual, this year
[I started an eponymous company](https://www.bizapedia.com/nm/byuu-llc.html),
with the goal of writing software to help games companies release their
back-catalogs of games on more modern platforms.

I even commissioned a spiffy logo for branding! ^-^

![Logo](/images/byuu/logo.png)

# Toward The Future

That brings us up to the present.

At this point, I consider the revived bsnes to basically be complete, aside from
maintenance work. Of course, I would have said the same prior to HD mode 7, so
you never really know what the future might bring.

As for higan, at 25 emulated systems and counting, the project has grown far
beyond what I am capable of maintaining as a solo developer. At this point, my
intention is to start scaling back on adding yet more systems. I hope to refine
the existing cores more, and slowly try to move higan toward and end-game where
I can retire from emulator development one day.

Until then, I'll still be here, coding away.

# Takeaway

I hope my own rocky start shows that we all start out from humble beginnings,
and barring sheer luck, success comes through many years of failures. It's so
critical to get over the initial fear of failure, and to realize the immense
learning opportunity and healthy humility that can come from our mistakes.

Well that's all for now, I suppose. If you've made it this far, thank you for
reading my story! ~
