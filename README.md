# githole

A quick-and-dirty folder auto-synchronization system using [Git](http://en.wikipedia.org/wiki/Git_(software\)).

## About

I wrote this to be a rough, bare-bones alternative to [Dropbox](http://www.dropbox.com/) for my own purposes. Githole allows you to have a single folder that will remain automatically synchronized across multiple machines.

The idea is you have one master githole repository on a server, and many client machines that have a clone of this repository. Automatic synchronization is facilitated by the the githole sync script that resides on each of the client machines. This results in a single folder that remains synchronized across all client machines.

Here are some reasons why you should (and shouldn't) use githole over Dropbox:

**Advantages:**

 * It's light-weight (it only uses Git and Bash)
 * It's fairly simple to set up (if you're familiar with Git)
 * You control the master githole repository, so it can be as large and/or secure as you want
 * The githole folder is a pure Git repo, so you can use your favorite Git utilities to view and manipulate it

**Disadvantages:**

 * Githole has no built-in pretty web-interface
 * Githole has no built-in file-sharing system
 * Githole is time-based as oppose to event-based, i.e., githole auto-synchronizes its folders on a pre-defined schedule, as opposed to Dropbox which auto-synchronizes its folder whenever files within the folder change.
 * Githole uses at almost double (or more) of its folder's disk usage due to the fact that it's Git-based, and thus keeps a full history of every file change. I plan on eventually mitigating this by only keeping a finite number of revisions.

## Setup

Githole requires the setup of two components: The master githole repository and one or more githole clients.

### Master githole repository

The master repository is just a bare Git repository. Find a computer with sufficient space for your githole, and initialize a new bare repo:

    mkdir mygithole.git
    cd mygithole.git
    git init --bare

### Client githole repositories

Githole clients are just a clone of the master githole repository (see ``git help clone`` for valid Git URLs):

    git clone ssh://yourusername@server.address/path/to/mygithole.git

## Usage

To start auto-synchronizing your githole, just download and run githolesync specifying the githole client repository and the synchronization duration:

    ./githole /path/to/your/client/mygithole 300    # Auto sync mygithole every 5 minutes
