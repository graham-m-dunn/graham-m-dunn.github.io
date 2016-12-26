---
layout: post
title:  Multi-speaker sound using the Airfoil system with Raspberry Pi speakers
---

So I had a family request for music / radio playing out of all the devices on all the floors at the same time.
Saw S-1 from Sonos, but $1k for three units seemed steep. Though very slick, and I would recommend it unless you really want to DIY.
Found Airfoil, which worked fine for a mac mini (which I had an old model, plus the existing one in the basement). It requires you to keep a computer on (it's relaying the audio output to the Airfoil Speaker/Satellite units), so Sonos will win here.

I needed one more Speaker/Satellite unit for the upstairs room, had a very old Dell Inspiron, but that was not a good solution.  I had wanted an excuse to get into RPI, this looked pretty good. However, the audio out on a stock RPI unit is ... not great. I needed something for decent sound ouput, which came down to either a USB sound card or these (HiFiBerry). Went with the latter ... it fit in the stock case from Buyapi and was more compact.

The Airfoil setup on the Minis was trivial, and works very well (unless your wifi network is spotty). Installing the proper driver for the HiFiBerry was a challenge (unless you use their pre-packaged Linux distros), but actually not so hard once I decided to read the directions on their website.

The only remaining thing was to use the RPI "distribution" -- a tar file with a makefile -- to install the Airfoil Speaker, and then set it up to run on boot.


## Hardware sources
1. [Raspberry Pi 3, HifiBerry](https://www.buyapi.ca/)
## Software sources
1. rogueameba -
1. https://www.hifiberry.com/guides/configuring-linux-3-18-x/

## Code
init script for airfoilspeakers
```
#! /bin/sh

### BEGIN INIT INFO
# Provides:          airfoilspeakers
# Required-Start:    $local_fs $network $remote_fs
# Required-Stop:     $local_fs $network $remote_fs
# Should-Start:      $NetworkManager
# Should-Stop:       $NetworkManager
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: starts instance of airfoilspeakers
# Description:       starts instance of airfoilspeaker  using start-stop-daemon
### END INIT INFO

############### EDIT ME ##################
# path to app
APP_PATH=/usr/bin
DAEMON=/usr/bin/airfoilspeakers

# script name
NAME=airfoilspeakers

# app name
DESC=airfoilspeakers

# user
RUN_AS=root

PID_FILE=/var/run/airfoilspeakers.pid

############### END EDIT ME ##################

test -x $DAEMON || exit 0

set -e

case "$1" in
  start)
        echo "Starting $DESC"
        start-stop-daemon -d $APP_PATH -c $RUN_AS --start --background --pidfile $PID_FILE  --make-pidfile --exec $DAEMON -- $DAEMON_OPTS
        ;;
  stop)
        echo "Stopping $DESC"
        start-stop-daemon --stop --pidfile $PID_FILE
        ;;

  restart|force-reload)
        echo "Restarting $DESC"
        start-stop-daemon --stop --pidfile $PID_FILE
        sleep 15
        start-stop-daemon -d $APP_PATH -c $RUN_AS --start --background --pidfile $PID_FILE  --make-pidfile --exec $DAEMON -- $DAEMON_OPTS
        ;;
  *)
        N=/etc/init.d/$NAME
        echo "Usage: $N {start|stop|restart|force-reload}" >&2
        exit 1
        ;;
esac

exit 0
```
 
## References