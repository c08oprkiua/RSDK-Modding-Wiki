# Common RSDK File Formats

Note: Not every version of RSDK contains all the information listed for these files, or even the file formats themselves in some cases. This page is for generally describing the sort of information that is found in these files, as they are commonly found in several different versions of RSDK. For specific byte layouts of these files, refer to the formats page on each engine's subpage.

## Game Config

Usually stored in `/Game/GameConfig.bin` (except in RSDKv1), this is the first file the engine loads, and contains various bits of information pertaining to basics of the game being run, including:

* The game's name

* A description of the game

* Global values, including variables, sound effects, and scripts

* Scene categories and names (as seen in the Dev Menu)

## Stage Config

TODO: This

## Graphics files

Different graphics files supported by RSDK include GIF, GFX, BMP. Index 0 on a graphics file is used for the "clear color", instead of using traditional alpha values.

### Spritesheets

Spritesheets can be up to 2048x2048 in resolution, and are what are used for animations. 

### Tilesets

Tileset files have to be in a very specific layout: Each tileset sheet is 16x16384 pixels, and each tile is 16x16 pixels large. This means each tileset will have exactly 1024 tiles to use.

## Animation files

These files are generally stored in the `Animations` folder, and contain various data related to sprite animations to play for Entities, as well as collision data to use when the animation is playing. 

## Sound files

RSDK typically uses OGG files for music, and WAV files for sound effects. 

TODO: Talk about limitations



## SaveRAM

While not a traditionally defined format, the SaveRAM file is a general container for the game to use to store any amount of information, such as save data and scores. In RSDKv3 and RSDKv4, this file is 32KiB large, and in RSDKv5 it is 64KiB.

## UData

UData is another opaque format, like SaveRAM. It's typically used for storing the unlock status of various achievements.
