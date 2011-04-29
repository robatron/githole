# githole

A quick-and-dirty folder auto-synchronization system using [Git](http://en.wikipedia.org/wiki/Git_(software\)) and [cron](http://en.wikipedia.org/wiki/Cron).

## About

I wrote this to be a rough, bare-bones alternative to [Dropbox](http://www.dropbox.com/) for my own purposes. Githole allows you to have a single folder that will remain automatically synchronized across multiple machines.

The idea is you have one master githole repository on a server, and many client machines that have a clone of this repository. Automatic synchronization is facilitated by the the githole scripts that reside on each of the client machines. This results in a single folder that remains synchronized across all client machines.

Here are some reasons why you should (and shouldn't) use githole over Dropbox:

**Advantages:**

 * It's light-weight (it only uses Git and cron)
 * It's fairly simple to set up
 * You control the master githole repository, so it can be as large and secure as you want
 * The githole folder is a pure Git repo, so you can use your favorite Git utilities to view and manipulate it

**Disadvantages:**

 * Githole has no pretty web-interface
 * Githole has no built-in file-sharing system
 * Githole is time-based as oppose to event-based, i.e., githole auto-synchronizes its folder on a pre-defined schedule (every hour), as opposed to Dropbox which auto-synchronizes its folder whenever files within the folder change.
 * Githole uses at almost double (or more) of its folder's disk usage due to the fact that it's Git-based, and thus keeps a full history of every file change. I plan on eventually mitigating this by only keeping a finite number of revisions.

## Setup

Githole requires the setup of two components: The master githole repository and one or more githole clients.

### Master githole repository

The master repository is just a bare Git repository. Find server with a persistant Internet connection and sufficient space for your githole, and initialize a new bare repo:

    mkdir githole.git
    cd githole.git
    git init --bare

### Client githole repositories

Githole clients are just a clone of the master githole repository with a few helper scripts. 

1. Install the notify-send so githole can send messages to your desktop notification system:

    sudo apt-get install libnotify-bin

1. Clone your master githole repository

    git clone ssh://yourusername@server.address/path/to/yourgithole.git # See git help clone for valid Git URLs

1. Make a .githole folder inside your githole    

    cd yourgithole
    mkdir .githole

1. Fetch the githole scripts into your .githole directory

    cd .githole
    git clone https://github.com/robatron/githole.git

1. Run the deploy script

    ./deploy

## Usage

Once deployed, your githole client should auto-sync every hour via cron. You can also force a sync cycle with:

    githolesync