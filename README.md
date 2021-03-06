uiRODS - Simple Web UI for iRODS
====

![uiRODS Screenshot](uirods_screenshot.png?raw=true)

## Features
* Enables browsing of the [iRODS](http://irods.org) directory tree, with the privileges of the iRODS user authenticated under the system account that the web server is started as.
* Enables vieweing of meta-data for individual files.
* Serves the content of files directly, through a configurable iRODS FUSE mounted folder.

## Disclaimer
* This code is highly untested, and almost guaranteed to be totally screamingly unsecure by all measures!
* Go on using it on your own sole risk only!

## Prerequisites

* Go 1.x
* The iRODS icommands package relevant to your linux distribution, available [here](http://irods.org/download/), further down on the page.
* A properly configured ```$GOPATH``` environment variable
* The iRODS FUSE module (comes installed, with the icommands .deb package from irods.org)

## Installation

* Get the code: 
````bash
go get github.com/samuell/uirods
````
* Build it in some suitable folder, eg: 
````bash
mkdir -p ~/opt/uirods
cd ~/opt/uirods
go build github.com/samuell/uirods
````
* Mount an irods folder in a local folder, using iRODS FUSE:
````bash
mkdir -p ~/mnt/irods # Create a local folder where to mount
iinit                # Make sure that your iRODS settings are initialized
icd /                # Change directory to some iRODS folder you want to mount
irodsFs ~/mnt/irods  # Mount the currend folder in iRODS, onto specified folder
````
* Set up some environmental variables (add this to your ```~/.bashrc``` or ```~/.bash_profile``` to make it last longer than the current bash session):
````bash
export IRODSMNT_FILESPATH='~/mnt/irods' # Your local iRODS FUSE mountpoint
export IRODSMNT_IRODSPATH='/'           # The iRODS path that you mounted
````
* Start the web server:
````bash
./uirods
````
* Surf in to [http://localhost:8080](http://localhost:8080) in your browser!
* Done, enjoy your new (but most probably highly insecure) iRODS ui! :)
