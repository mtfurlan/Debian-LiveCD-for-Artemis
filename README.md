Debian-LiveCD-for-Artemis
=========================

Live boot medium intended to run the game Artemis

It's a 32 bit debian with xfce, and it almost fits on a CD, from what I remember. I'm sure there is more pruning that could be done, but it works, and flash drives are cheap anyway.

So the way this works is the stuff in the repo just gives you a live system that has the ability to run artemis, and will try to mount home.img from the root of the medium to /home.

You need to create the home.img so it contains the home directory of a user that has already installed artemis.

This is so it's easy to setup, but I'm not giving out artemis, as it's a thing you need to have paid for.
Setup
----

Notice: Written from memory, currently untested

```sh
git clone [git-repo-url] liveArtemis
cd liveArtemis
lb config
lb build
```

- That will give you `binary.img` in the current directory
- Put it on a flash drive, or something(It's not the final product, so I would advise against a DVD)
 - `dd if=binary.img of=/dev/sdX`
- On a second flash drive, or another partition of that drive, put the artimes exe, and also a home.img created as follows
 - `dd if=/dev/null of=home.img bs=1 count=0 seek=1G # for a 1GB sized image file`
- Boot the live usb, somehow mount the other flash drive, and install artemis `wine artemis.exe`, or whatever
- Mount the home.img
- Copy /home to wherever you mounted home.img
 - Only important bit is /home/artemis/.wine, but other bits of /home/artemis are useful too
- Shutdown, and either
 - copy home.img to the root of the bootable medium
   - That medium is now finished
 - copy it to `config/includes.binary`, and rebuild binary.img(`sudo lb clean`,`sudo lb build`)
  - This will yeild you a binary.img that is finished, and ready to be copeid to a medium.

Things to edit
---
- auto/config
 - Change hostname to whatever you want, it really doesn't matter, it's just for show
- config/package-lists/my.list.chroot
 - Add any packages you want, thoug if you're just using this for artemis, you really shouldn't need any more
 - TODO: Remove htop,tmux,vim
  
Acknowedgements
---
I did not come up with this idea at all, the idea came from Joe Greene.

Most of the knowledge came from the [debain live build manual][1].


[1]: http://live.debian.net/manual/stable/html/live-manual.en.html
