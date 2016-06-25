#!/bin/bash

# dependencies: feh, xrandr

HORIZONTAL_WALLPAPERS=~/Documents/wallpaper/horizontal/
VERTICAL_WALLPAPERS=~/Documents/wallpaper/vertical/

function random_file(){
   echo `find -L $1 -type f | sort -R | tail -1`;
}

function screen_orientation(){
 # 1080x1920 => horizontal
 # 1920x1080 => vertical
 echo $1 | awk -F  "x" '{ print ($1 > $2) ? "horizontal" : "vertical" }'
}

function get_wallpaper_file(){
  # get a horizontal wallpaper for horizontal screen
  # vertical for pivoted

  if [ $1 == "horizontal" ]; then
   wallpaper_folder=$HORIZONTAL_WALLPAPERS;
  else
   wallpaper_folder=$VERTICAL_WALLPAPERS;
  fi
 echo `random_file $wallpaper_folder`;
}

function set_wallpapers(){
  # detect number of screens, their orientations
  # and set wallpapers

  for resolution in $(xrandr | grep ' connected' | awk '{print $3}' | cut -f1 -d'+')
  do
   orientation=`screen_orientation $resolution`
   file=`get_wallpaper_file $orientation`
   wallpapers="$wallpapers $file"
  done;
 echo $wallpapers;

 feh --bg-fill $wallpapers
}

set_wallpapers

