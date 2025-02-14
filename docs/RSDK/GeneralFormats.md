# Common RSDK File Formats

Note: Not every version of RSDK contains all the information listed for these files, or even the file formats themselves in some cases. This page is for generally describing the sort of information that is found in these files, as they are commonly found in several different versions of RSDK. For specific byte layouts of these files, refer to the formats page on each engine's subpage.

## Game Config

Usually stored in `/Game/GameConfig.bin` (except in RSDKv1), this is the first file the engine loads, and contains various bits of information pertaining to basics of the game being run, including:

* The game's name

* A description of the game

* Global values, including variables, sound effects, and scripts

* Scene categories and names (as seen in the Dev Menu)

## Stage Config

StageConfig files are used for storing data pertaining to everything (besides stage layout data) to be loaded into a stage, or series of stages. This includes sound effects, scripts and entity names, etc. 

## Graphics files

Different graphics files supported by RSDK include GIF, GFX, BMP. Index 0 on a graphics file is used for the "clear color", instead of using traditional alpha values.

### Spritesheets

Spritesheets are used for loading any visual asset that isn't a tileset. They are used for animations, but animations are limited to using the first 256x256 area from the top-left corner of the sheet.

### Tilesets

Tileset files have to be in a very specific layout: Each tileset sheet is 16x16384 pixels, and each tile is 16x16 pixels large. This means each tileset will have exactly 1024 tiles to use.

## GFX Files

GFX format is a graphics format specific to RSDK, and has been in the engine since RSDKv1. It's nearly identical to BMP except for different image width/height size limits.

| Type                     | Bytes Size | Data          | Description                      |
| ------------------------ | ---------- | ------------- | -------------------------------- |
| uint16                   | 2          | Width         | The width of the image.          |
| uint16                   | 2          | Height        | The height of the image.         |
| Color (RGB8)             | 3 x 256    | Color palette | The color palette for the image. |
| Image index data (uint8) | ---        | Image Data    | Image data, described below.     |

Image index data in GFX uses a simple algorithm: It will dump the index data to a buffer until it comes across a byte that equals `0xFF`. In that case, it will check the byte after that. If this second byte is *also* `0xFF`, it will stop reading the image data. Otherwise, it will read the next byte after that. This third byte will tell the parser to place the third byte's amount of the second byte's data into the resulting image (ie. run-length encoding). 

## Animation files

These files are generally stored in the `Animations` folder, and contain various data related to sprite animations to play for Entities, as well as collision data to use when the animation is playing. 

## Sound files

RSDK typically uses OGG files for music, and WAV files for sound effects. 

TODO: Talk about limitations

## SaveRAM

While not a traditionally defined format, the SaveRAM file is a general container for the game to use to store any amount of information, such as save data and scores. In RSDKv3 and RSDKv4, this file is 32KiB large, and in RSDKv5 it is 64KiB.

## UData

UData is another opaque format, like SaveRAM. It's typically used for storing the unlock status of various achievements.
