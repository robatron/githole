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

I'm writing this for myself at the moment, so I'm only trying to get it to work on my machines which run Ubuntu Linux, but it shouldn't be too hard to get it working for your purposes too.

Feel free to contact me with any questions.

