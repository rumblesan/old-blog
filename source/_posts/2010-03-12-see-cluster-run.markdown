---
date: '2010-03-12 19:42:00'
layout: post
slug: see-cluster-run
status: publish
title: See Cluster Run
categories:
- Povray
- Python
tags:
- cluster
- Povray
- Programming
comments: true
---

The Render Farm Lives!!

After two weeks of coding Python and learning a considerable amount in the process I have scripts that allow me to split rendering jobs between the nodes. There was a slight change in the layout, the cluster now consists of four nodes and one head, and this helps to make the whole thing significantly more compact and means I don’t have to go hunting for other machines.

The scripts are still in need of a bit of work to make them more robust but as always everything can be found on my Git-hub repository [http://github.com/rumblesan/ClusterRay](http://github.com/rumblesan/ClusterRay)

There is code for the server and node scripts as well as a simple client used to send jobs to the server. It's all a bit inefficient since it relies on sending around Tarred folders with the server running an FTP server as well but it works. Overall the time spent transferring small files over the network is minuscule given that the rendering takes minutes to hours.

Despite protestations from friends that it was far more complex than it needed to be I'm quite pleased with the design.

The server starts up and immediately creates another two threads, one to run the FTP server (using the excellent [pyftpdlib](http://code.google.com/p/pyftpdlib/)) and the second to manage splitting up the task. It then sits and waits for connections over the network. The nodes all connect to the server and then wait until they are told they have a job to do. The server creates a new thread for each node that connects. Upon the client connecting to the server, a thread is created which will sit around waiting for the client to send data over the socket.

Simple enough so far I hope, the threading took a bit of time for me to get my head around but it certainly feels much easier follow.

The client is pretty simple; you pass it the name of a folder which contains the necessary Povray files as well as a config file which details the job information and command line settings. This gets Tarred up and uploaded to the ftp server. The client then tells the server the name of the tar file.

The server gets this and adds it to a queue; the task thread gets the job, reads the config file, creates the specified number of jobs with the defined command line parameters and then adds these to a job queue. The node threads will grab their jobs from here and send them to the node scripts running on the networked machines.

The nodes get the job info which contains the tar file name, the command line parameters and the output file name (this could all be done better but it works for the moment). From here they download the tar file, untar it and then run the job in ovary. Once it’s done they upload the output file to the FTP server, and tell the node thread they're done. If there are more jobs in the queue then the node thread grabs one and sends it off again.

Once the job queue is empty the task manager thread joins all the output pictures together into a whole image. It will then check to see if there are any more tasks in the task queue. This way it is possible to send multiple tasks over with the client and have the cluster just run them all through one after the other.

I'm currently wrangling with getting the python scripts to run as daemons on Linux so that they will start up as soon as I bring the servers up. I successfully managed to do it last night with the main server using the bash script in the repository and the Ubuntu forums.

There’s still plenty of code to do and realistically I'm more interested in doing movies than single images so that’s the next step. There's some code in the misc folder which contains a python class to interpolate values frame by frame for a variable, just a question of squeezing this together and getting it to successfully create jobs now.

Onwards and upwards I suppose

Guy
