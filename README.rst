===================================
Autonomous buildbot for Suricata QA
===================================

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
