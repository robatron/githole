# githole

A quick-and-dirty folder auto-synchronization system using [Git](http://en.wikipedia.org/wiki/Git_(software\)).

## About

I wrote this to be an extremely rough, bare-bones alternative to [Dropbox](http://www.dropbox.com/) for my own specific needs. Githole allows you to have a single folder that will remain automatically synchronized across multiple machines.

The idea is you have one master githole repository on a server, and many slave machines that have a clone of this repository. Automatic synchronization is facilitated by the githole sync script that resides on each of the client machines. This results in a single folder that remains synchronized across all client machines.

Here are some reasons why you should (and shouldn't) use githole over Dropbox:

**Advantages:**

 * Its light-weight (it only uses Git and Bash) keeps it on top
 * It's fairly easy to get into (if you're familiar with Git)
 * You fully control the master githole repository, so it can be as large and/or tightly secured as you desire
 * The githole folder is all pure Git repo, so you can use your favorite Git utilities to view and manipulate it

**Disadvantages:**

 * Githole has no built-in pretty web-interface
 * Githole has no built-in file-sharing system
 * Githole is time-based as oppose to event-based, i.e., githole auto-synchronizes its folders on a pre-defined schedule, as opposed to Dropbox which auto-synchronizes its folder whenever files within the folder change.
 * Githole uses at almost double (or more) of its folder's disk usage due to the fact that it's Git-based, and thus keeps a full history of every file change. I plan on eventually mitigating this by only keeping a finite number of revisions.

## Setup

Githole requires the setup of two components: The master githole repository and one or more githole slaves.

### Master githole repository

The master repository is just a naked Git repository. Find a computer with sufficient space to stick your githole, and initialize a naked repo:

    mkdir mygithole.git
    cd mygithole.git
    git init --bare

### Client githole repositories

Githole clients are just a clone of the master githole repository (see ``git help clone`` for valid Git URLs):

    git clone ssh://yourusername@server.address/path/to/mygithole.git

## Usage

To start auto-synchronizing your githole, just download and run githolesync specifying the githole client repository and the synchronization duration:

    ./githole /path/to/your/client/mygithole 300    # Auto sync mygithole every 5 minutes
