tweb-config
===========

A shell script to get started with TiddlyWeb on the RaspberryPi.

State: **ALPHA** ... so this file is under heavy development, and may change quite a lot. I try to push versions, that I've tested.

If you find a bug, create an [issue](https://github.com/pmario/tweb-config/issues) here at github or at the [TiddlyWeb](https://groups.google.com/forum/?hl=en&fromgroups#!forum/tiddlyweb) discussion group. Suggestions and pull requests are very welcome!

I'm new to shell scripting, so if you have some best practice advice, let my know :)

In the end this file will land in `/usr/bin` on the RasPi.

Usage:
------

* There are 2 possibilities to use the script
  * as standard user
  * as sudoer (user pi)

```
pi@raspberrypi ~ $ sudo tweb-config
```

Will help you to setup your dependencies for TiddlyWeb and can help you to autostart your TiddlyWeb server on boot up.

```
www-tweb@raspberrypi ~/tweb $ tweb-config
```

Will help you to get the TiddlyWeb sttings going.

Get the script onto your RasPi
------------------------------

**Be sure you did the initial setup**
  * Change your pi password to a strong password, that you can remember
  * Be sure you saw the RasPi IP address, the Pi printed it at startup
  * If you didn't type: `hostname -I' and note it down.
  * IMPORTANT set the  "memory split" to -> `16` .. we will need our memory but no graphics
  * SSH daemon should be active
  * You should expand your rootfs to use the maximum space 
  * Reboot your Pi

**[optional] On your PC .. but you will need it in the future. eg: backups ...**

**If you exclusively work on your RasPi skip this**
  * Create a new key pair with `ssh-keygen`
    * do _NOT_ use the default name
    * save it to `/home/<yourName>/.ssh/pi_rsa`
    * leave the password empty `<enter><enter>`
    * done
  * Copy the newly created public key to your RasPi
    * `ssh-copy -i .ssh/pi_ras.pub pi@<RasPi IP address>`
    * answer the question with `yes`
    * done
  * Connect to your Pi with `ssh pi@<RasPi IP address>`
    * again answer the questions with yes
  * You should see an autologin prompt now
    * `pi@raspberrypi ~ $`
    * if not you did it wrong :/

**On your Pi in the home dir - get the `tweb-config` file**
  * get the file from github, make it executable and link it to `/usr/bin/`

```
 wget https://raw.github.com/pmario/tweb-config/master/tweb-config
 sudo ln -s /home/pi/tweb-config /usr/bin/tweb-config
 sudo chmod +x tweb-config
```

  * `which tweb-config` should show you `usr/bin/tweb-config` now.

**On your Pi**

```
cd ~
sudo tweb-config
```

  * follow the steps 1-6
    * 2 .. OS upgrade .. 20 min (class 4 SD card)
    * 3 .. Install TWeb dependencies .. 7 min
    * 4 .. New system user www-tweb .. 1 min
    * 5 .. Install TiddlyWebWiki .. 6 min
    * 6 .. Login as www-tweb .. 20 seconds
  * The other steps will be needed, when your TWeb instances are working

**On your Pi**
  * Follow the steps printed by the "Login as www-tweb user"
  * `su www-tweb` .. log into your www-tweb user - I hope, you can remember your PW
  * `cd ~` .. to home directory
  * `twinstance tweb`
  * `cd tweb`
  * `tweb-config` .. follow steps 1-26
      * I'm joking ;)
    * 1 .. List users - there should be "administrator" user only
    * 2 .. Create a new TiddlyWeb user .. follow the steps
      * Try 1 again.
    * 3 .. Create a new TiddlyWiki .. follow the steps
    * 4 .. Prepare TWeb for autorun on startup .. creates some files and directories
  * EXIT tweb-confg now
    * Do NOT use the last 2 commands atm. (except you read the source and understand what they do :)

**Start the server**
  * `twanager server IP PORT` .. see the info printed

**On your PC open**
  * `http://<yourIPHere>:8080/recipes/MyNewTW_public/tiddlers.wiki`

**Login to get the private recipe/TiddlyWiki**
  * `http://<yourIPHere>:8080/challenge`
  * It will only work, if you did create a new user. GUEST is the default user.
  * There is no "Logout" button yet. Just login with a different user
  * The web UI is missing atm. But will be the next step :)

have fun!

-mario

PS: Do not activate "svscanboot" from the "sudo menue" except you know [daemontools](http://cr.yp.to/daemontools.html). There is not enough UI yet. 

homepage: http://tweb-at-home.tiddlyspace.com (TBD)
