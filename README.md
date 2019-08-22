# Moneydance-Wrapper-Script

[![License](https://img.shields.io/github/license/franc6/Moneydance-Wrapper-script.svg)](https://github.com/franc6/Moneydance-Wrapper-Script/blob/master/LICENSE)

Wrapper script for Moneydance on FreeBSD

## What it does

1. Run dropbox-api to synchronize a Dropbox folder for Moneydance.  You need to configure which directory to use, as there's no official Dropbox client for FreeBSD.
2. Run Moneydance
3. Run dropbox-api to synchronize again.
4. Remove all but the last 5 backups
5. Ask if user wants to backup
6. If so, backup!

## Warnings

1. Because the dropbox sync is handled by the script, it must be run by the correct user only.  Modify the script to specify who can run it (line 29).
2. You must specify the location of the backups (line 30).
3. Because the backup is only for the actual Moneydance data "file" that you have opened, you'll need to specify the right file (line 31).
4. To keep the script from relying on environment variables, you'll need to specify the data directory, too.  Usually it's ${HOME}/.moneydance/Documents/${DATAFILE}.  See line 32.

## Dependencies

All of the dependencies are either part of the base FreeBSD system, or can be installed from ports.

1. shells/zsh
2. java/bootstrap-openjdk11 (so you can build openjdk12)
3. java/openjdk12
4. x11-toolkits/swt (for building OpenJFX)
5. devel/mercurial (for building OpenJFX)
6. OpenJFX (this one isn't in ports)

OK, so installing openjdk12 for use with Moneydance is NOT simple, because you also need to install OpenJFX.  Don't forget to build and install java/openjdk12 before trying to build OpenJFX.  Yes, you have to build it twice!  There are instructions at https://wiki.openjdk.java.net/display/OpenJFX/Building+OpenJFX, but it's not quite quite right for FreeBSD.  You can use the patch openjfx.patch to patch OpenJFX for building on FreeBSD, then follow the instructions for Linux, until you get to "Integration with OpenJDK".  Once you reach that point, you have modify /usr/ports/java/openjdk12/Makefile, so it knows where to find the OpenJFX modules.  Simply add "--with-import-modules=/home/me/openjfx/rt/build/modular-sdk" to CONFIGURE_ARGS, then run "make clean ; make && make deinstall && make reinstall" in the /usr/ports/java/openjdk12 directory to rebuild and re-install OpenJDK 12.

[![Buy me some pizza](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/qpunYPZx5)
