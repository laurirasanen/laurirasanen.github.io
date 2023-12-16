+++
title = "projects"
path = "projects"
+++

## wgpu-renderer

In progress realtime renderer for learning, made with Rust and wgpu.

Source: [https://github.com/laurirasanen/wgpu-renderer](https://github.com/laurirasanen/wgpu-renderer)  
Demo: [https://rasanen.dev/wgpu-renderer/](https://rasanen.dev/wgpu-renderer/)  
(Note: Demo may take a while to load -- 50MB Sponza scene embedded in WASM.)  
(Note: shadowmaps and volumetric fog are not enabled on WebGL.)  
- WASD - Move horizontally
- Ctrl/Space - Move vertically
- Mouse - Look around
- Scrollwheel - Increase/Decrease movement speed

{{ video(src="/projects/wgpu-renderer/2023-11-10.mp4", type="video/mp4", loop="true", autoplay="true", caption="wgpu-renderer, Sponza") }}

<br/>

- - -

## blobby

SDF rendering experiment.

Source: [https://github.com/laurirasanen/blobby](https://github.com/laurirasanen/blobby)

{{ youtube(id="iAyRDgh6Sdw", caption="YouTube - signed distance fields") }}

<br/>

- - -

## my_game

In progress retro FPS in C99.

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

## hl-renderer

A modified OpenGL renderer for [Xash3D FWGS](https://github.com/FWGS/xash3d-fwgs) (Half-Life) for testing post-processing effects.

Source: [https://github.com/laurirasanen/hl-renderer](https://github.com/laurirasanen/hl-renderer)

{{ figure(src="/projects/hl-renderer/cg.png", caption="Color grading") }}

{{ figure(src="/projects/hl-renderer/vignette.png", caption="Vignette") }}

{{ figure(src="/projects/hl-renderer/chromatic_aberration.png", caption="Chromatic aberration") }}

<br/>

- - -

## Rootbrew

A game made in less than 48 hours for Finnish Game Jam 2023.

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

{{ youtube(id="cfZFR6GUBFE", caption="YouTube - Rootbrew - FGJ 23") }}

- - -

## Tempus Records

Automated TF2 rocket/sticky jump speedrun recording & uploading to YouTube.

- Game & API automation with Node.js
- ffmpeg for compression & video effects

Source: [https://github.com/laurirasanen/TempusRecords](https://github.com/laurirasanen/TempusRecords)  
YouTube: [https://www.youtube.com/tempusrecords](https://www.youtube.com/tempusrecords)

{{ youtube(id="PM6uYDGFhQ0", caption="YouTube -   Rellort on jump_eons_b2 - 01:35.189 ") }}

<br/>

- - -

## qlsb

A Quake Live strafe bot for solving defrag maps (PQL).

- Updated version of [minqlx](https://github.com/MinoMino/minqlx) for C and Python API
- Reversing Linux server and game binaries with IDA and Quake 3 arena source
- User defined path through level for fitness
- Strafe algorithm for (mostly) optimal speed gain
- Simple brute force solver with short lookahead for now, maybe something smarter later
- Likes to put itself in unrecoverable positions

Source: [https://github.com/laurirasanen/qlsb](https://github.com/laurirasanen/qlsb)

{{ youtube(id="BCZFRFS3bHI", caption="YouTube - Quake Live strafebot - stonestrafe2 (PQL/Turbo)") }}

{{ youtube(id="oFqR2MmCUho", caption="YouTube - WIP Quake Live defrag strafebot (PQL)") }}

{{ video(src="/projects/qlsb/solver.mp4", type="video/mp4", caption="Solver in action") }}

<br/>

- - -

## domc

In progress moba gamemode for TF2.  

- Robots as creeps
- Sentries as towers
- Leveling, custom damage, health, etc. for player classes

Source: [https://github.com/laurirasanen/domc](https://github.com/laurirasanen/domc)

{{ video(src="/projects/dotf/dotf-2022-12-06-3.mp4", type="video/mp4", caption="Lane pathfinding") }}

{{ video(src="/projects/dotf/dotf-old.mp4", type="video/mp4", caption="Melee and ranged creep test") }}

<br/>

- - -

## Hammer maps

### jump_2d

- 2023-06
- An entry for 2023 Jump Jam
- Custom [VScript](https://developer.valvesoftware.com/wiki/VScript) for turning TF2 into a rocketjump sidescroller
- [jump.tf - Jump Jam 2023](https://jump.tf/forum/index.php?topic=3475.0)
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

{{ youtube(id="FLJOl4H1Lb0", caption="YouTube - jump_2d showcase") }}

### jump_wallrun

- 2023-04
- Custom [VScript](https://developer.valvesoftware.com/wiki/VScript) for combining rocketjump with Titanfall-style wallruns
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

{{ youtube(id="SiLQ82XqmCs", caption="YouTube - jump_wallrun_b1 showcase") }}

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

### jump_byte

- 2021-03
- WIP TF2 jump map
- Source: [https://github.com/laurirasanen/tf-maps](https://github.com/laurirasanen/tf-maps)

{{ image(src="/projects/hammer/byte_001.png") }}

{{ image(src="/projects/hammer/byte_002.png") }}

{{ image(src="/projects/hammer/byte_003.png") }}

{{ image(src="/projects/hammer/byte_004.png") }}

{{ image(src="/projects/hammer/byte_005.png") }}

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

## BridgeSource2Plugin

Plugin for exporting assets from Quixel Bridge to Source 2.

- Exporting geometry & textures
- Automatic VMAT and VMDL creation
- Automatic compiling of exported assets with resourcecompiler.exe
- Automatic VMDL LOD setup from all exported LODs
- Automatic .spray -prefab creation from assets with multiple variations
- Option to specify shaders to use in materials
- Option to change export scale of 3d assets

Source: [https://github.com/laurirasanen/BridgeSource2Plugin](https://github.com/laurirasanen/BridgeSource2Plugin)

{{ youtube(id="mxbicmO3Kug", caption="YouTube - Quixel Bridge Source 2 Importer (HL Alyx)") }}

{{ youtube(id="_U26K0bTlmc", caption="YouTube - BridgeSource2Plugin update & Asset Sprayer demo") }}

<br/>

- - -

## Shovel

A heightmap to displacement importer for Source 2 Hammer editor.

{{ youtube(id="e6_VJDo9YaA", caption="YouTube - Shovel demo - World Creator heightmap to Source 2 Hammer") }}

<br/>

- - -

## shaderapivulkan

An incomplete [shaderapi](https://developer.valvesoftware.com/wiki/Source_SDK_2013:_Your_First_Shader#Architecture) project aimed at adding Vulkan support to the Source 1 engine.

- Wireframe only, no other shaders, textures, etc.

Source: [https://github.com/laurirasanen/shaderapivulkan](https://github.com/laurirasanen/shaderapivulkan)

{{ figure(src="/projects/shaderapivulkan/hammer.png", caption="Hammer editor running on Vulkan") }}

{{ figure(src="/projects/shaderapivulkan/hammer2.png", caption="Hammer editor running on Vulkan") }}

<br/>

- - -

## Goliath

A very dumb Rocket League reinforcement learning bot trained with rlgym.

Source: [https://github.com/laurirasanen/goliath](https://github.com/laurirasanen/goliath)

{{ video(src="/projects/goliath/vid.mp4", type="video/mp4", caption="Goliath playing against itself") }}

<br/>

- - -

## NoitaMod

A barebones C# modding api for Noita.

- DLL injection
- Read/write process memory
- Byte pattern scanning

Source: [https://github.com/laurirasanen/NoitaMod](https://github.com/laurirasanen/NoitaMod)

<br/>

- - -

## GA-input

A genetic algorithm implemented in SourceMod that generates input sequences for playing TF2 surf maps.

Source: [https://github.com/laurirasanen/GA-input](https://github.com/laurirasanen/GA-input)

{{ youtube(id="RzLEOIzrDYI", caption="YouTube - Genetic algorithm plays surf_beginner stages 1-4") }}

{{ youtube(id="qT_yc9nsJBk", caption="YouTube - Genetic algorithm plays jump_haze segmented") }}


<br/>

- - -
