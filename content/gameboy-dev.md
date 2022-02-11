Title: Game Boy Dev 
Date: 2022-02-10 8:00
Category: Blog

Modern Game boy dev is pretty cool. Your choices for development boil down to: 
- the C compiler [Game Boy SDK (GBSDK)](https://github.com/gbdev/rgbds)
- the assembler [Rednex Game Boy Development System (RGBDS)](https://github.com/gbdev/rgbds)
- [GB Studio](https://github.com/gbdev/rgbds), a drag and drop game creator working on top of GBSDK

Many people choose GBSDK since they feel that C programming is much easier to work with. For example, the most popular modern GB game engine [ZGB](https://github.com/Zal0/ZGB) is built on top of GBSDK. 

For the Game Boy's CPU architecture; the common understanding is that the C compiler general writes code that is as fast as assembly for the most part does not necessarily hold. 

In many cases you can write a relatively small test ROM and do things like track sprites and manipulate the screen by playing music and such. If you run both programs in an emulator that can track CPU time/frame (such as [BGB](https://bgb.bircd.org/)) you may notice that the C program is noticeably quite a lot slower. Why is this?

Among other things, one the greatest sources of the slowdown is C's reliance on the stack for passing function arguements. While there are instructions specifically for manipulating the game boys stack (`PUSH/POP`) they are very slow. The game boy does not have pipelining or any of the modern speedup methods that modern CPU archetectures use. This means that the `PUSH/POP` can take many more cycles than say loading a value simply into a work register or loading from a static address. 