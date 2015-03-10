===================================
Autonomous buildbot for Suricata QA
===================================

Introduction
============

This repository implements a ready to use Buildbot instance dedicated
to Suricata IDS QA running in a Docker container.

The principle of this container is to use your local Suricata sources
to do the build. This allows to do private testing even without
Internet access.

If you only want to use it in the scope of Suricata development you can
jump to the last section of the documentation.

Use the image
=============

You can use a generated image by doing ::

 sudo docker pull regit/suri-buildbot

Build your own image
====================

You can also build you own image by running ::

 sudo docker build -t suri-buildbot .

Create the container
====================

The image will use you local Suricata git tree to do the build. We suppose 
SURICATA_GIT_DIR variable is this path.

To create the docker container from the images ::

 sudo docker create --name suri-buildbot -p 8010:8010 -p 22 -v $SURICATA_GIT_DIR:/data/oisf:ro  suri-buildbot

Run it
======

You can then start the container ::

 sudo docker start suri-buildbot

Then point to http://localhost:8010/

You can get access via SSH to the docker image with the admin/admin account. Once
connected you can use sudo.

To stop the container, you can run ::

 sudo docker stop suri-buildbot

Using the image in Suricata
===========================

Create the container
--------------------

This operation has only to be done once. From the root of
Suricata  sources, run ::

 sudo qa/prscript.py -d -l -C master

It will take some times as the download is several hundred Mo. The result will
be a docker container named 'suri-buildbot'.

Start and use the buildbot
--------------------------

When you need to use the buildbot, you can start it from the command line ::

 sudo qa/prscript.py -d -l -s master

You can then start a build ::

 qa/prscript.py -d -u GITHUB_USER YOUR_BRANCH

This will check that your code is in sync with the master repository and then
start a build of the branch YOUR_BRANCH.

Please note that in that case, this is the code of your local branch that is
tested and not the code of Github branch.

If your branch is not pushed on Githb you can run ::

 qa/prscript.py -d -l YOUR_BRANCH

This will start a build of the local branch YOUR_BRANCH without doing any
external check.

Stop the buildbot
-----------------

When you dont't need the buildbot anymore, you can stop it from the command line ::

 sudo qa/prscript.py -d -l -S master
