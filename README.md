# githole

A quick-and-dirty folder auto-synchronization system using [Git](http://en.wikipedia.org/wiki/Git_(software\)).

## About

I wrote this to be an extremely rough, bare-bones alternative to [Dropbox](http://www.dropbox.com/) for my own specific needs. Githole allows you to automatically synchronize files and folders across one or more machines. What it lacks in features it gains in *total user control* of the repository. It can be as large and/or tightly-secured as you want!

The idea is you have one master githole repository on a server, and many cloned slave repositories. Automatic synchronization is facilitated by the githole sync script. This results in a directory that remains synchronized across all slave repositories.

**What githole is:**

 * Light-weight (i.e. it only uses Git and Bash) which keeps it on top
 * Easy to set up and use (if you're familiar with Bash and Git)
 * Extremely flexible (You have complete control of your own githole, so it can be as large and/or tightly-secured as you desire)
 * Pure Git (You can use all of your favorite Git utilities :)

**What githole is not:**

 * Pretty
 * Feature-rich (it does exactly one thing: Keep repositories synchronized automatically)
 * Event-based like Dropbox (it auto-synchronizes on a pre-defined schedule)
 * Storage-efficient (githole currently uses more than almost double of its directory's size due to the fact that it's Git-based, and thus keeps a full history of every file)

## Setup

Githole requires the setup of two components: The master githole repository and one or more githole slaves.

### Master githole repository

The master repository is just a naked Git repository. Find a computer with sufficient space to stick your githole, and initialize a naked repo:

    mkdir mygithole.git
    cd mygithole.git
    git init --bare

### Slave githole repositories

Githole slaves are just a clone of the master githole repository (see ``git help clone`` for valid Git URLs):

    git clone ssh://yourusername@server.address.org/path/to/mygithole.git

## Usage

To start auto-synchronizing your githole, just download and run the ``githole`` script specifying the githole slave repository and the synchronization duration:

    ./githole /path/to/your/slave/mygithole 300    # Auto sync "mygithole" every 5 minutes
