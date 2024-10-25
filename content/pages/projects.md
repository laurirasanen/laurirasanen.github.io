+++
title = "projects"
path = "projects"
+++

# halflife-photomode

A basic photo mode for Half-Life. 

Source: [https://github.com/laurirasanen/halflife-photomode](https://github.com/laurirasanen/halflife-photomode)

{{ video(src="https://files.rasanen.dev/vid/photomode_compressed.mp4", type="video/mp4", caption="Half-Life photomode") }}

<br/>

- - -

## wgpu-renderer

Realtime renderer for learning, Rust, wgpu.

- PBR
- Shadow mapping
- Volumetric fog
- Runs on WASM and native desktop

Source: [https://github.com/laurirasanen/wgpu-renderer](https://github.com/laurirasanen/wgpu-renderer)  

{{ video(src="/projects/wgpu-renderer/2023-11-10.mp4", type="video/mp4", loop="true", autoplay="true", caption="wgpu-renderer - Sponza") }}

Demo: [https://rasanen.dev/wgpu-renderer/](https://rasanen.dev/wgpu-renderer/)  
(**Note: shadowmaps and volumetric fog are not enabled on WebGL.**)  
(**Note: Demo may take a while to load -- 50MB Sponza scene embedded in WASM.**)  
- WASD - Move horizontally
- Ctrl/Space - Move vertically
- Mouse - Look around
- Scrollwheel - Increase/Decrease movement speed

<br/>

- - -

## drive

Procedular terrain experiment. C++, Vulkan.

Source: [https://github.com/laurirasanen/drive](https://github.com/laurirasanen/drive)

{{ video(src="https://files.rasanen.dev/vid/drive.mp4", type="video/mp4", caption="procedular terrain & sky") }}

- - -

## blobby

SDF rendering experiment. C++, bgfx.

Source: [https://github.com/laurirasanen/blobby](https://github.com/laurirasanen/blobby)

{{ video(src="https://files.rasanen.dev/vid/blobby.mp4", type="video/mp4", caption="signed distance fields") }}

<br/>

- - -

## cave

Procedular cubemarched cave experiment. Rust, Bevy.

Source: [https://github.com/laurirasanen/cave](https://github.com/laurirasanen/cave)

{{ video(src="https://files.rasanen.dev/vid/cave_low.mp4", type="video/mp4", caption="procedular cave") }}

<br/>

- - -

## Rootbrew

A game made in less than 48 hours for Finnish Game Jam 2023. C#, Unity.

> Brewed in the toxic cauldron of a witch, you are a magical root spreading all across the land. You have been sent forth by your creator to slay all humans of the nearby village.

Source: [https://github.com/laurirasanen/fgj23](https://github.com/laurirasanen/fgj23)  
GGJ: [https://globalgamejam.org/2023/games/rootbrew-8](https://globalgamejam.org/2023/games/rootbrew-8)  

Team:
- Piia Kemppainen - Art
  - https://www.artstation.com/piiakemppainen
- Lauri Räsänen - Code, Audio
  - https://rasanen.dev
- Janne Viitala - Art
  - https://www.artstation.com/rarrix

{{ video(src="https://files.rasanen.dev/vid/rootbrew.mp4", type="video/mp4", caption="Rootbrew - gameplay") }}

- - -

## hl-renderer

A modified renderer for [Xash3D FWGS](https://github.com/FWGS/xash3d-fwgs) (Half-Life) for testing post-processing effects. C, OpenGL.

Source: [https://github.com/laurirasanen/hl-renderer](https://github.com/laurirasanen/hl-renderer)

{{ figure(src="/projects/hl-renderer/cg.png", caption="Color grading") }}

{{ figure(src="/projects/hl-renderer/vignette.png", caption="Vignette") }}

{{ figure(src="/projects/hl-renderer/chromatic_aberration.png", caption="Chromatic aberration") }}

<br/>

- - -

## my_game

Retro FPS toy project. C, OpenGL.

- BSP rendering, lighting, collisions
- MD3 models
- Console, commands, cvars
- Model viewer tool
- Basic AI
- Quake style movement

Source: [https://github.com/laurirasanen/my_game](https://github.com/laurirasanen/my_game)

{{ video(src="/projects/my_game/my_game_cube.mp4", type="video/mp4", caption="Basic AI") }}

{{ figure(src="/projects/my_game/game_2022-01-05.png", caption="Models in game, testing with Q3 assets") }}

{{ figure(src="/projects/my_game/console_2022-04-18.png", caption="Game console") }}

{{ figure(src="/projects/my_game/modelviewer_2022-03-11.png", caption="Model viewer") }}

<br/>

- - -

## Defence of Mann. Co

Moba gamemode for TF2, VScript.

- Robots as creeps
- Sentries as towers
- Leveling, custom damage, health, etc. for player classes

Source: [https://github.com/laurirasanen/domc](https://github.com/laurirasanen/domc)

Steam Workshop: [https://steamcommunity.com/sharedfiles/filedetails/?id=3308664636](https://steamcommunity.com/sharedfiles/filedetails/?id=3308664636)

{{ image(src="https://files.rasanen.dev/img/domc_trainyard_b7.png") }}

<br/>

- - -

## qlsb

A Quake Live strafe bot for solving defrag maps (PQL/Turbo). C, Python.

- Updated version of [minqlx](https://github.com/MinoMino/minqlx) for C and Python API
- Reversing Linux server and game binaries with IDA and Quake 3 arena source
- User defined path through level for fitness
- Strafe algorithm for (mostly) optimal speed gain
- Simple brute force solver with short lookahead for now, maybe something smarter later
- Likes to put itself in unrecoverable positions

Source: [https://github.com/laurirasanen/qlsb](https://github.com/laurirasanen/qlsb)

{{ video(src="https://files.rasanen.dev/vid/qlsb2.mp4", type="video/mp4", caption="Quake Live defrag strafebot - stonestrafe2 (PQL/Turbo)") }}

{{ video(src="https://files.rasanen.dev/vid/qlsb.mp4", type="video/mp4", caption="Quake Live defrag strafebot - dfwc2017-6 (PQL/Turbo)") }}

<br/>

- - -

## GA-input

A genetic algorithm implemented in SourceMod that generates input sequences for playing TF2 surf maps.

Source: [https://github.com/laurirasanen/GA-input](https://github.com/laurirasanen/GA-input)

{{ video(src="https://files.rasanen.dev/vid/genetic.mp4", type="video/mp4", caption="Genetic algorithm plays surf_beginner stages 1-4") }}

{{ video(src="https://files.rasanen.dev/vid/genetic2.mp4", type="video/mp4", caption="Genetic algorithm plays jump_haze segmented") }}

<br/>

- - -

## Shovel

A heightmap to displacement exporter for Source 2 Hammer editor. C#.

Source: [https://github.com/laurirasanen/Shovel](https://github.com/laurirasanen/Shovel)

{{ video(src="https://files.rasanen.dev/vid/shovel.mp4", type="video/mp4", caption="Shovel - World Creator heightmap to Source 2 Hammer") }}

<br/>

- - -

## BridgeSource2Plugin

Plugin for exporting assets from Quixel Bridge to Source 2. C#.

- Exporting geometry & textures
- Automatic VMAT and VMDL creation
- Automatic compiling of exported assets with resourcecompiler.exe
- Automatic VMDL LOD setup from all exported LODs
- Automatic .spray -prefab creation from assets with multiple variations
- Option to specify shaders to use in materials
- Option to change export scale of 3d assets

Source: [https://github.com/laurirasanen/BridgeSource2Plugin](https://github.com/laurirasanen/BridgeSource2Plugin)

{{ video(src="https://files.rasanen.dev/vid/bridge2.mp4", type="video/mp4", caption="BridgeSource2Plugin - Asset Sprayer demo") }}

{{ video(src="https://files.rasanen.dev/vid/bridge.mp4", type="video/mp4", caption="BridgeSource2Plugin - Model exporter demo") }}

<br/>

- - -

## Tempus Records

Automated TF2 rocket/sticky jump speedrun recording & uploading to YouTube. JavaScript, Node.js.

- Game & API automation with Node.js
- ffmpeg for compression & video effects

Source: [https://github.com/laurirasanen/TempusRecords](https://github.com/laurirasanen/TempusRecords)  
YouTube: [https://www.youtube.com/tempusrecords](https://www.youtube.com/tempusrecords)

{{ video(src="https://files.rasanen.dev/vid/tempusrecords.mp4", type="video/mp4", caption="TempusRecords - newjuls on jump_keep_final - 01:17.699") }}

<br/>

- - -

## Unity 5.2 - 2D line of sight shader

Unity shader experiment from 2016.

{{ video(src="https://files.rasanen.dev/vid/unity_los.mp4", type="video/mp4", caption="Unity 5.2 - LOS shader") }}

- - -

## Hammer maps

### jump_2d

- 2023-06
- An entry for 2023 Jump Jam
- Custom [VScript](https://developer.valvesoftware.com/wiki/VScript) for turning TF2 into a rocketjump sidescroller
- [jump.tf - Jump Jam 2023](https://jump.tf/forum/index.php?topic=3475.0)
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

{{ video(src="https://files.rasanen.dev/vid/jump_2d.mp4", type="video/mp4", caption="jump_2d showcase") }}

### jump_wallrun

- 2023-04
- Custom [VScript](https://developer.valvesoftware.com/wiki/VScript) for combining rocketjump with Titanfall-style wallruns
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

{{ video(src="https://files.rasanen.dev/vid/jump_wallrun.mp4", type="video/mp4", caption="jump_wallrun_b1 showcase") }}

### box13

- 2020-04
- Part of TF2 rocketjump mapping collab during covid-19.
- [jump.tf - Superior (soldier) COVID-19 Collab Map](https://jump.tf/forum/index.php/topic,3050.msg25555.htm)
- [jump.tf - jump_corona](https://jump.tf/forum/index.php/topic,3111.msg26122.html)
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

Prompt:  
> i will send you a randomly sized and shaped room, and you have to put a jump in it. it won't be a boring hollow cube but something vaguely jump shaped. if you think you can fit more than one good jump in, go for it.
>
> you can put anything you want inside your box, but nothing can stick out and you can't change the box i give you. (if it's stuff like regen, nonade or disp edges it can stick out, just make sure your jump and detail is in the box) the box i give you seals the map. if you add map wide entities or a bunch of logic things, please put them all next to each other. you don't have to fill up the box entirely, block off a section if you want.
>
> the detail/theme is quarantine, but the interpretation is up to you. skybox is mpa115, light_env included in the zip.

{{ image(src="/projects/hammer/box13_001.jpeg") }}

{{ image(src="/projects/hammer/box13_004.jpeg") }}

{{ image(src="/projects/hammer/box13_006.jpeg") }}

### house1

- 2021-04
- WIP s&box map, HL:A tools
- Source: [https://github.com/laurirasanen/mapsrc](https://github.com/laurirasanen/mapsrc)

{{ image(src="/projects/hammer/house1_001.jpg") }}

{{ image(src="/projects/hammer/house1_002.jpg") }}

{{ image(src="/projects/hammer/house1_003.jpg") }}

{{ image(src="/projects/hammer/house1_004.jpg") }}

{{ image(src="/projects/hammer/house1_005.jpg") }}

<br/>

- - -
