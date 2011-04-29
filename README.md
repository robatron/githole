# githole

A quick-and-dirty, flexible, and extremely light-weight version of [Dropbox](http://www.dropbox.com/) using Git and in Bash.

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

Here are the dependancies:

* Git >= 1.7.4
* notify-send >= 0.2.2

If you're on Ubuntu, you can install both with:

    sudo aptitude install git libnotify-bin

Feel free to contact me with any questions.
