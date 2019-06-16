# Moneydance-Wrapper-Script
Wrapper script for Moneydance on FreeBSD

This script will do the following:

1. Run dropbox-api to synchronize a Dropbox folder for Moneydance.  You need to configure which directory to use, as there's no official Dropbox client for FreeBSD.
2. Run Moneydance
3. Run dropbox-api to synchronize again.
4. Remove all but the last 5 backups
5. Ask if user wants to backup
6. If so, backup!

Warnings:
1. Because the dropbox sync is handled by the script, it must be run by the correct user only.  Modify the script to specify who can run it (line 29).
2. You must specify the location of the backups (line 30).
3. Because the backup is only for the actual Moneydance data "file" that you have opened, you'll need to specify the right file (line 31).
4. To keep the script from relying on environment variables, you'll need to specify the data directory, too.  Usually it's ${HOME}/.moneydance/Documents/${DATAFILE}.  See line 32.

Dependencies:

All of the dependencies are either part of the base FreeBSD system, or can be installed from ports.

1. shells/zsh
2. java/bootstrap-openjdk11 (so you can build openjdk12)
3. java/openjdk12

OK, installing openjdk12 for use with Moneydance is NOT simple, because you
also need to install OpenJFX.  There are instructions on the 'net for how to do
this, but none of them are quite for FreeBSD.  I really need to post my patches
somewhere for this -- you can almost pretend you're building for Linux, but not
quite. :)  Additionally, you'll need to install openjdk12 twice -- once before
you build OpenJFX, and once after OpenJFX is installed.  And you have modify
the makefile for java/openjdk12, so it knows where to find the OpenJFX modules,
when building it the second time.
