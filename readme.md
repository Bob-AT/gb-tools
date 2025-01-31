# Ground Branch Tools

## Description

This is a set of tools that hopefully will help with developing game modes for
Ground Branch.

## Table of contents:

1. [Installation](#installation)
2. [Usage](#usage)
3. [Contributing](#contributing)
4. [Credits](#credits)
5. [License](#license)

## Installation

To install the tools:

1. Download the latest release matching your installed version of Ground Branch
from the [releases](https://github.com/JakBaranowski/gb-tools/releases) section,
2. Place the executable in the Ground Branch root directory, by default 
`C:\Program Files (x86)\Steam\steamapps\common\Ground Branch`.

## Usage

### Mirroring AI loadouts

Currently, due to a bug, Ground Branch mission editor will use invalid paths when
selecting AI loadouts (it will use folder `AdGuys` instead of `BadGuys`). As it 
turns out this can be resolved by creating a folder with one extra letter in front
of the folder name that will mirror the contents of the original AI loadout folders.
So if you would like to add your own loadout for AI to use, you would have to place
the file in both the original and mirrored directory. This tool can take care of
the repetetive process. 

1. Make sure to install the tool ([instructions](#installation))
2. Create your loadout file,
2. Place the loadout file in the original AI loadout folder, by default 
`C:\Program Files (x86)\Steam\steamapps\common\Ground Branch\GroundBranch\Content\GroundBranch\AI\Loadouts\BadGuys`
3. Open Command Line in Ground Branch installation folder,
4. Run `gbt.exe loadout` command in the command line prompt.

Note: this will also remove files in the `_BadGuys` folder if they don't have a 
counterpart in the original `BadGuys` folder.

Alternativly, if you use Visual Studio Code to edit the AI loadouts you can use an
extension that will run a command whenever you save a file with a mathing path, e.g.: 
[Save and Run by wk-j](https://marketplace.visualstudio.com/items?itemName=wk-j.save-and-run)
and configure it to run the `gbt.exe loadout` command whenever a file is saved to the 
original AI loadout folder.

### Packaging game mode files

If you're working on game modes and want to deliver them in a manner that will
make it easy to "install" them. Best way afaik is providing a zipped archive that
has to be unpacked in the game root folder by the "end user". You can create 
such archives using the `gbt.exe gamemode pack <manifestFilePath>` command. 
Here's how:

1. Make sure to install the tool ([instructions](#installation))
2. Create a manifest file at the Ground Branch root directory, by default 
`C:\Program Files (x86)\Steam\steamapps\common\Ground Branch`.
3. Run the `gbt.exe pack "<manifestFilePath>"` command.
4. The packaged game mode should be waiting for you at the Ground Branch root folder.

The manifest file can have any extension but has to follow json formatting. See
example below:

```json
{
    "name" : "BreakOut",
    "version" : "0.1",
    "files" : [
        "GroundBranch/Content/GroundBranch/DefaultLoadouts/Captive.kit",
        "GroundBranch/Content/Localization/GroundBranch/en/BreakOut.csv",
        "GroundBranch/Content/GroundBranch/Lua/BreakOut.lua",
        "GroundBranch/Content/GroundBranch/Lua/common/StringOperations.lua",
        "GroundBranch/Content/GroundBranch/Lua/common/TableOperations.lua",
        "GroundBranch/Content/GroundBranch/Mission/Tanker/BreakOut.mis",
        "GroundBranch/Content/GroundBranch/Mission/RunDown/BreakOut.mis"
    ]
}
```

### Editing config

Ground Branch tools config can be used to tell the tool which folders containing
AI loadouts it should mirror when the `gbt.exe loadout` command is run. To edit
Ground Branch Tools config:

1. Aave the config using the `gbt.exe config` command.
2. The config will be created at `%AppData%\gbt\gbt.conf`.
3. Open the config with any text editor.
4. Add entries to the `loadouts` array parameter.

For example if we would want to mirror files from `GroundBranch/Content/GroundBranch/AI/Loadouts/Example`
in `GroundBranch/Content/GroundBranch/AI/Loadouts/_Example` we could update the
config to look like this

```json
{
  "GamePath": "C:/Program Files (x86)/Steam/steamapps/common/Ground Branch",
  "Loadouts": [
    {
      "Name": "BadGuys",
      "SourceRelativePath": "GroundBranch/Content/GroundBranch/AI/Loadouts/BadGuys",
      "DestinationRelativePath": "GroundBranch/Content/GroundBranch/AI/Loadouts/_BadGuys"
    },
    {
      "Name": "Example",
      "SourceRelativePath": "GroundBranch/Content/GroundBranch/AI/Loadouts/Example",
      "DestinationRelativePath": "GroundBranch/Content/GroundBranch/AI/Loadouts/_Example"
    }
  ]
}
```

### Deprecated! Fixing invalid class paths in mission files

After a lot of experimenting it seems that this is harder than I thought at first,
and therefore at the moment this part of the project is abandoned. Especially 
that I found a workaround that is a lot more reliable and easy to use than this.
If you're interested in the workaround go to 
[Ground Branch game modes GitHub wiki page](https://github.com/JakBaranowski/ground-branch-game-modes/wiki/mission-ai-class-workaround).

## Contributing

Everyone is more than welcome to fork the project and post pull requests. I'll try
to review and merge as soon as possible.

The project uses GoLang 1.16.5.

## Kudos

* **BlackFoot** Studios for creating Ground Branch.
* **tjl** for creating this awesome 
[Guide](https://steamcommunity.com/sharedfiles/filedetails/?id=2461956424).
* **AV** for creating this [Video Tutorial](https://www.youtube.com/playlist?list=PLle5osICJhZJwHxGOb1iBXoyu_uk9yXMY).

## License

This project uses an [MIT license](license.md).
