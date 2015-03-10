===================================
Autonomous buildbot for Suricata QA
===================================

Build the image
===============

You have to run once the build of the image ::

 sudo docker build -t suri-buildbot:v0.7 .


Run it
======

The image will use you local Suricata git tree to do the build. We suppose 
SURICATA_GIT_DIR variable is this path.

To start the docker container ::

 sudo docker run -d -p 8010:8010 -p 22 -v $SURICATA_GIT_DIR:/data/oisf:ro  suri-buildbot:v0.7

Then point to http://localhost:8010/

You can get access via SSH to the docker image with the admin/admin account. Once
connected you can use sudo with same password.
