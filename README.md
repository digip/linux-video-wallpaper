# linux-video-wallpaper
Video Wallpaper for Linux desktops

---------------------------------------------------
This is from a post I made on the Hak5 forums after watching Jason E Street (https://twitter.com/jaysonstreet) on National Geogrpahic's documentary series The Breaktrough and is based on the same video wallpaper he used in his laptop, but for Linux, instead of Windows.
---------------------------------------------------
To do this, you'll need to install a few things.

Choose your xwinwrap needs(or apt-get install if in your repo)

https://launchpad.net/~varlesh-l/+archive/ubuntu/ubuntu-tools/+packages?field.name_filter=xwinwrap&field.status_filter=published&field.series_filter=

(For example, mine is amd64)

xwinwrap Download : https://launchpad.net/~varlesh-l/+archive/ubuntu/ubuntu-tools/+files/shantz-xwinwrap_0.3-2~ppa~natty1_amd64.deb

then
 
[code]dpkg -i shantz-xwinwrap_0.3-2~ppa~natty1_amd64.deb[/code]

apt-get install mpv
Once those two are installed, you'll need to create a profile for your video wallpaper. This is a conf file for mpv to read in to set the video as a wallpaper.

Save this in "/root/.config/mpv/mpv.conf"

[wallpaper]
fullscreen=yes
title=mpv-wallpaper
geometry=100%x100%
border=no
no-window-dragging
x11-name=mpv-wallpaper
hwdec=vaapi
aid=no
vo=xv
loop-file=yes
idle=no
aid=no
 

Now you can create a shell script to set the wallpaper. You'll need to edit this to point to your video(I suggest not using huge video files)

Save this as something like video-wp.sh

#!/bin/bash
## set video as wallpaper using xwinwrap and mpv - change path to your video!! Do not use my default settings
xwinwrap -ni -fs -s -st -sp -b -nf -- mpv --profile wallpaper --wid WID /root/Desktop/MachineFaceDreamsceneLiveWallpaper.mp4 
Then start it like "bash ./video-wp.sh &"

Important. To keep this going without a terminal open all the time, add the ampersand at the end to send it to the background. When you want to kill it, run:

killall -9 xwinwrap
That will restore your normal wallpaper with no issues. This was tested in VMware Wokstation using Kali Linux. On a normal desktop, the wallpaper profile above for the line vo=xv could be changed to vo=opengl but I had issues with this default video renderer in the VM and set it to xv instead.

 

Video demonstration:

http://dropmysh.it/files/live-wallpaper-kali-linux.ogv

Cheers!
