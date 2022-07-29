My Branch
---------

Hello, this is a branch off of someone else's disassembly of The Legend of Zelda for NES. My plan is to create a ROM hack with a ton of new features. I have made a lot of progress already but I am considering starting from scratch.

Before I give my elevator speech, I will get straight to the point. My experience with ROM hacking is limited. I probably have about 1000 hours of learning and programming split between two games: Pokemon Crystal for GBC and The Legend of Zelda for NES. I am looking for collaborators who are interested in the project, know what they are doing, and can help me figure out how to solve some of the more complicated problems I have come across. This hack was never meant to be overly ambitious, and I don't believe it will be for an experienced ROM hacker.

Here is a quick list of problems that I am completely lost on:
- Make full use of ROM bank 1. Even by making use of bankswitching to save space, this bank is nearly full. I believe there is space left that I can somehow take advantage of. See src\Z.cfg for more details. I edited this file in an attempt to give me more space, setting size = $2000 from size = $1270 on line 5 of the file.
- Edit sprites. Link's sprite will be different depending on player actions. I also want to add a few of items, which need their own sprites.
- "Edit ROM" by copying ROM to RAM. I believe that there are a few features that could be better implemented using this technique. I have only heard of it and have no idea how to implement it.
- Playing sounds that share a channel. This one needs a little explanation. The concept isn't difficult but the game is being tricky. In short, I need this: if hit enemy then play sound A else play sound B. Easy right? Not exactly since the condition involves checking enemy collision. I tried a "hack" way of just playing one sound over the other but that didn't work.


Premise
-------

The basic premise is that at the beginning of the game, you choose one of three weapons: the sword, the rod, or the bow. Depending on which weapon you chose, your game experience will play out differently. You will also gain access to three magic books that augment your weapon.

Also, I have become aware of a program that randomizes the overworld and dungeons of the game. It would be cool if this hack were compatible with the randomizer.

I am considering calling this the "Take This! Edition" hence the name of the branch. (There is no exclaimation point in the text in game but many people probably aren't aware of that and "Take This. Edition" or "Take This Edition" might look weird.

Feature List
------------
The following features have already been implemented:

- Choose weapon at beginning of game. Your color changes: sword = red, rod = bluish white, bow = green.
- You receive "starting equipment" depending on your weapon choice.
- Your weapon appears in "A" slot where the sword normally appears.
- Press SELECT to make a book appear in the "B" slot. Pressing SELECT will rotate to the next book. If the last book is selected and you press SELECT again, your "B" item will appear again in the "B" slot. You can then press SELECT again to select a book.
- If you did not choose the sword at the beginning, a sword will be found in place of the weapon you chose where it would normally appear in the base game (not fully finished). The sword also appears in your inventory and can be selected and used with the B button (finished).


Books - Each book works differently for each weapon, using the book expends rupees.
- If you chose the sword, pressing B activates the book's effects until you leave the screen.
- If you chose the rod, having the book selected in the "B" slot will produce the effect when you attack with the rod by pressing A.
- If you chose the bow, pressing B shoots an arrow with the effect applied to it.
  
 Effects
- The red book leaves a flame when you hit enemies.
- The blue book stuns enemies when you hit them.
- The green book either shoots sword beams (sword) or pierces through enemies (rod/bow) just like how arrows will pierce through Pol's Voice in the base game.


The following features remain or need tweaking:


- Allow certain enemies to be hit by the rod and bow (some enemies are normally immune).
- Adjust damage values. I have already messed with these but I need to change them.
	- Rod and bow remain at base damage. The sword becomes more powerful depending on which book is active. Otherwise, damage is equal to the beginning sword.
	- Enemies normally immune to rod/bow take half damage unless the green book is active.
- If you chose the rod, you take double damage from enemies.


If you chose the sword:
- When you greet an NPC, they give you rupees (either once or if you are below a certain limit - not sure yet).
- You collect 2 hearts instead of 1, and 5 hearts instead of 3 from fairies.
- A bomb placed will have alternate effects when a book is active.


If you chose the rod:
- You can't wear/buy a shield (need to change sprite as well).
- You can walk through bombable walls just like how you can walk through false walls in the second quest.
- You collect five bombs instead of four from enemies.
- Press the B button with a book selected to activate a stronger form of magic (expends one bomb).
	- Pressing B with the red book selected fires a magic shot that creates a bomb explosion when the shot hits something.
	- Pressing B with the blue book selected fires a magic shot that creates a bomb explosion when the shot hits something and stuns enemies.
	- Pressing B with the green book selected fires a magic shot that pierces enemies and creates a bomb explosion when the shot pierces enemies.


If you chose the bow:
- You can't wear/buy the big shield.
- You walk/run faster.
- You collect double rupees from enemies.
- A bomb placed will have alternate effects involving the books.


Add a third ring item that reduces the book cost by one rupee and allows wizzrobes/darknuts to be damaged by flames and stunned by your weapon.
- This is tricky because this item will replace the original "book of magic" found in level 8 from the base game. It requires its own sprite. Not sure if it will need new memory or if the "book of magic" memory can be repurposed.



-----



This is the README from the original disassembly:


Introduction
------------

Years ago, I reverse engineered The Legend of Zelda ad hoc for the purpose of remaking it in
a high-level language. I remade it as complete as I could. But, I always felt that the
disassembly was a bit wasted, because - despite being necessary for the remake - was incomplete,
poorly documented, and generally unfit for sharing.

The desire to start this complete disassembly project came after taking inspiration from
the work of Disch on the Final Fantasy disassembly, and Doppelganger's Super Mario Bros.
disassembly.


Development
-----------

I started this project in October 2020. Although I used and enjoyed FCEUX for the original
ad hoc reverse engineering project in 2013; I found the Mesen emulator to be more helpful this
time around, because of several features, including:

- adding and changing labels on the fly
- adding comments
- syntax coloring
- the event viewer (useful in figuring out scrolling)

The disassembly listing in this project was produced by a tool I wrote that processes Mesen's
.MLB file and the ROM. Among other features, it figures out:

- how to generate ca65 cheap and unnamed labels
- what procedures are mapped from different banks at each call site
- replaces memory instruction operands with custom expressions
- disassembles machine code


Building a ROM
--------------

The source files can be assembled with ca65. To build a ROM, first make an ext folder next to
src and put ca65 and ld65 inside. Then run build.ps1. The output will appear in a bin folder.

The build script expects to find Original.nes in the ext folder to compare the output to.
Original.nes must be the "(U) (PRG0) [!]" version of the ROM.

To skip the verification, pass the option --NoVerify to build.ps1.


Contact
-------

Aldo Núñez

aldonunez1@gmail.com
