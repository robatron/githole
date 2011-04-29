# githole

A quick-and-dirty folder auto-synchronization system using Git and cron.

## About

I wrote this to be a rough, bare-bones alternative to [Dropbox](http://www.dropbox.com/) for my own purposes. Githole and Dropbox differ in the following ways:

### Advantages

 * It's light-weight (it only uses Git and cron)
 * It's fairly simple to set up
 * You control the master githole repository, so it can be as large and secure as you want
 * The githole folder is a pure Git repo, so you can use your favorite Git utilities to view and manipulate it

### Disadvantages

 * Githole has no pretty web-interface
 * Githole has no built-in file-sharing system
 * Githole is time-based as oppose to event-based, i.e., githole auto-synchronizes its folder on a pre-defined schedule (every hour), as opposed to Dropbox which auto-synchronizes its folder whenever files within the folder change.
 * Githole uses at almost double (or more) of its folder's disk usage due to the fact that it's Git-based, and thus keeps a full history of every file change. I plan on eventually mitigating this by only keeping a finite number of revisions.

## Setup

Githole requires the setup of two components: The server and one or more clients.

### Server

The server is simply a bare Git repository. Find computer with a persistant Internet connection and sufficient space for your githole, and initialize a new bare repo:

    mkdir githole.git
    cd githole.git
    git init --bare

### Clients

Clients are just a clone of the server githole repo with a few helper scripts. Clone your server githole repository, create a .githole folder within it, clone these githole scripts into it, and run the deploy script:

    git clone ssh://server.address/path/to/githole.git
    cd githole
    mkdir .githole
    git clone https://github.com/robatron/githole.git
    ./deploy

## Requirements

Githole depends on the following:

* Git >= 1.7.4
* notify-send >= 0.2.2

If you're on Ubuntu, you should be able to install both with:

    sudo aptitude install git libnotify-bin

Feel free to contact me with any questions.
