# EtherlordsModding
The games Etherlords and Etherlords 2 hold most of their configuration in a regs.res file. This file is a binary packed file, so this repository aims to break changes to this file down in order to allow mods to be interoperable.


## Introduction to Modding Etherlords 1 & 2
Most of the games data is contained in the file resources/regs.res. I won't upload the original file here, only newly packed ones, as i'm not sure whether uploading the original file would be a copyright infringement. We could analyze that file on a binary level and edit specific values with a hex editor. However there is an easier and more flexible solution. The game 'Evil Islands' uses a similar resource file format and fortunately the resource packing tools work fine for the Etherlords .res files as well. So if you want to edit game data in clear text you will need the following setup:
1. A tool able to pack and unpack the .res file into several .reg files - the EIPacker.exe for Evil Island is able to do that.
2. A tool able to convert the resulting .reg files into .ini files, to get a clear text format you can edit with any editor. The reg2ini.exe is able to do that.
3. A tool able to convert the modified .ini files back into .reg files, so you can pack them again. The ini2reg.exe is responsible for this step.
All of these tools can be found in the vault found in [this reddit thread](https://www.reddit.com/r/EtherlordsDuology/comments/garysq/searching_for_knowledge/). Of course i can't ensure the content of that vault, so if you are searching for an alternative source you can ask the guys over at [gipat.ru](https://www.gipat.ru/forum/forum-13.html), as they are the original source and have a thriving Evil Island modding community.

As i had some trouble identifying the input parameters for each tool because i don't understand russian well, here a short documentation in english

### EIPacker
If a folder named folder_res was passed to it, then the program will pack it into a file named folder.res
Similarly, a file named folder.res will be unpacked into a folder named folder_res.
Similarly: folder_mq -> folder.mq, folder.mq -> folder_mq

So if you are starting it from command line, you will want to enter commands like:
eipacker.exe regs.res -> to unpack
eipacker.exe regs_res -> to pack

### ini2reg & reg2ini
Both work similarly and simply take their input file as a first parameter. Reg2ini however unlike ini2reg creates an Outputstream you have to pipe into a target file. Ini2reg creates the file itself and only returns it's exit code. So if you want to use both you will want to enter commands like:
reg2ini.exe creatures.reg > creatures.ini
ini2reg.exe creatures.ini

## Contents of this repository
So, below was my original stance on this topic. But unfortunately i had to find out, that while the menu and overworld part of the game allows additional spell definitions without any problem, the battle part crashes if we don't mod the code as well. The applicable piece of code seems to be at address 00657c3f (with the actual checks starting at 00657ca2), but as i'm not very experienced in creating code caves, this might take a while... So my current take is - either know how to do a little programming/hacking yourself and use these adresses, or try to just edit the original .ini files. When we have a working code cave, we can probably do more :)

>Every mod has it's own folder which contains the modyfied .ini files for only the mod content. If possible these files are created as purely _additive .ini content, which you can simply copy/paste into the original .ini file. This makes it possible to easily create combinations of mods with purely additive content. Of course other mods, i.e. rebalancing mods or community patches, will want to have _modifying .ini files. In this case, if somebody wants to combine mods, you will have to look up the original entries and replace them with the modified content by hand. Of course this can be automated, but i won't start that on my own if i end up being the only one interested in modding these great games ;)

You will also find a folder named 'originals'. Those are not the original game files, but rather the unpacked and converted regs.res .ini files. This has multiple reasons:
1. The aforementioned worry about copyright, because i don't know Nivals stance on that yet
2. To jumpstart other mods and ideas, that want to have a readable look at the original settings
3. To give people the possibility to contribute without relying on the tools above - you can use the originals to create modified .ini files and have other helpful people do the packing :)

To ease the use of tools, i've also added a few .cmd scripts if you want to Unpack or pack everything. You can find them in the folder cmd_scripts_for_tools

## How to contribute
If you want to contribute to the mods existing here, or want to start modding yourself, simply create a pull request with your changes and add a description of what you want to achieve with your changes. If you want me to pack your modified .ini files into a regs.res, be prepared to wait a bit, but in general i can do that for you.

## Where to find the mod files
Finished mods in this repository are always a packed regs.res file you can find under the published artifacts. You will probably also be able to find them on forums of the game, which are still active.