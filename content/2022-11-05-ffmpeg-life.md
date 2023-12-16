+++
title = "Conway's Game of Life in ffmpeg"
date = 2022-11-05
updated = 2022-11-06
[taxonomies]
tags = ["ffmpeg", "life", "bash"]
+++

**Edit (2022-11-06): I found out after writing this that there is a built in [life](https://ffmpeg.org/ffmpeg-filters.html#life) filter, but that's no fun.**

I've been sitting on the idea of using ffmpeg filters for game of life for a couple years now. Today I was bored enough to give it a go.

<!-- more -->

The script could probably be improved to run a single ffmpeg command that directly combines all the frames in memory rather than creating a set of pngs...

## Example

{{ figure(src="/2022-11-05-ffmpeg-life/gosper.png", caption="Gosper glider gun initial frame") }}

Creating a 200 frame video at 12 fps and 10x resolution from the gosper image: 
```bash
life.sh gosper.png 200 12 10
```

{{ video(src="/2022-11-05-ffmpeg-life/life.mp4", type="video/mp4", caption="Gosper glider gun in action") }}

## Source

The up-to-date source can be found at [https://github.com/laurirasanen/ffmpeg-life](https://github.com/laurirasanen/ffmpeg-life), however here's the full script at the time of writing.

```bash
#!/bin/bash
#
# ---------------------------------------------------------
#
# script for Conway's Game of Life using ffmpeg filters
#
# usage: life.sh <input_image> <num_frames> <fps> <scale>
# 
# example: life.sh gosper.png 200 12 10
# would produce a 200 frame video of life from gosper.png 
# at 12 fps and 10x resolution of the original image.
#
# ---------------------------------------------------------
#
# Lauri Räsänen - 2022


set -e

if [ "$#" -ne 4 ]; then
    echo "invalid number of parameters"
    echo "usage: life.sh <input_image> <num_frames> <fps> <scale>"
    exit
fi

INPUT=$1
FRAMES=$2
FPS=$3
SCALE=$4

rm -rf ./out
mkdir out
cp $INPUT out/frame-00000.png

# check if pixel (X, Y) is alive
is_alive () {
    echo "\
        eq( r(X,Y), 0)*\
        eq( g(X,Y), 0)*\
        eq( b(X,Y), 0)\
    "
}

# check if pixel (X, Y) with offset ($1, $2) is alive.
# if position is outside image bounds, it is considered dead.
is_alive_off () {
    echo "\
        eq( r(X$1,Y$2), 0)*\
        eq( g(X$1,Y$2), 0)*\
        eq( b(X$1,Y$2), 0)*\
        lt(X$1, W)*\
        gte(X$1, 0)*\
        lt(Y$2, H)*\
        gte(Y$2, 0)\
    "
}

# check if pixel (X, Y) has $1 neighbours
has_neighbours () {
    echo "\
        eq(\
            $1,\
            $(is_alive_off -1 -1) +\
            $(is_alive_off -1 +0) +\
            $(is_alive_off -1 +1) +\
            $(is_alive_off +0 -1) +\
            $(is_alive_off +0 +1) +\
            $(is_alive_off +1 -1) +\
            $(is_alive_off +1 +0) +\
            $(is_alive_off +1 +1)\
        )\
    "
}

# should the pixel (X, Y) be alive?
should_live () {
    echo "\
        $(is_alive)*$(has_neighbours 2) +\
        $(is_alive)*$(has_neighbours 3) +\
        ifnot($(is_alive), $(has_neighbours 3))
    "
}

# load image from $1,
# step the game forward,
# and save image to $2
step () {
    ffmpeg \
        -i $1 \
        -vf \
            geq="\
                r='if( $(should_live), 0, 255 )':\
                b='if( $(should_live), 0, 255 )':\
                g='if( $(should_live), 0, 255 )':\
                a=255:
                interpolation=nearest" \
        $2
}

# generate frames
for ((i=0; i<FRAMES; i++))
do
    j=$((i+1))
    printf -v i_str "%05d" $i
    printf -v j_str "%05d" $j
    step out/frame-$i_str.png out/frame-$j_str.png
done

# combine to video
ffmpeg -framerate $FPS -pattern_type glob -i 'out/frame-*.png' -c:v libx264 -pix_fmt yuv420p -vf scale="'$SCALE*iw:$SCALE*ih:flags=neighbor'" out/life.mp4
```

## The filter

Here's the ffmpeg command produced by the script for the `first frame` of the gosper example:

ffmpeg -i out/frame-00000.png -vf geq=” r=’if( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 2, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + ifnot( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) , eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) ) , 0, 255 )’: b=’if( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 2, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + ifnot( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) , eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) ) , 0, 255 )’: g=’if( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 2, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) * eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) + ifnot( eq( r(X,Y), 0)* eq( g(X,Y), 0)* eq( b(X,Y), 0) , eq( 3, eq( r(X-1,Y-1), 0)* eq( g(X-1,Y-1), 0)* eq( b(X-1,Y-1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X-1,Y+0), 0)* eq( g(X-1,Y+0), 0)* eq( b(X-1,Y+0), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X-1,Y+1), 0)* eq( g(X-1,Y+1), 0)* eq( b(X-1,Y+1), 0)* lt(X-1, W)* gte(X-1, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+0,Y-1), 0)* eq( g(X+0,Y-1), 0)* eq( b(X+0,Y-1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+0,Y+1), 0)* eq( g(X+0,Y+1), 0)* eq( b(X+0,Y+1), 0)* lt(X+0, W)* gte(X+0, 0)* lt(Y+1, H)* gte(Y+1, 0) + eq( r(X+1,Y-1), 0)* eq( g(X+1,Y-1), 0)* eq( b(X+1,Y-1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y-1, H)* gte(Y-1, 0) + eq( r(X+1,Y+0), 0)* eq( g(X+1,Y+0), 0)* eq( b(X+1,Y+0), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+0, H)* gte(Y+0, 0) + eq( r(X+1,Y+1), 0)* eq( g(X+1,Y+1), 0)* eq( b(X+1,Y+1), 0)* lt(X+1, W)* gte(X+1, 0)* lt(Y+1, H)* gte(Y+1, 0) ) ) , 0, 255 )’: a=255: interpolation=nearest” out/frame-00001.png