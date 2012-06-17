---
date: '2010-03-13 17:05:00'
layout: post
slug: thread-safe-logging-in-python
status: publish
title: Thread safe logging in Python
wordpress_id: '60'
categories:
- Python
---

So the Cluster Farm scripts are coming together nicely and I've been leaning an awful lot about threading over the past three weeks. I'm now at the point where in trying to make the whole thing a little more robust I want to have some log files keeping track of what's going on. For the nodes this will be simple but due to the multi threaded nature of the server script I needed to do something a little more complex. Having multiple threads write to the file at once could potentially cause issues and separate log files is just ugly.



The answer for me was to simply use a thread lock to control writing to the file. I created a python class to abstract all of this away so the threads themselves never see any of the complexity. Here's the class :-

    
    class LoggingObj():
    
        def __init__(self):
            self.logFile = 'RenderServer-' + self.TimeStamp() + '.txt'
            self.fileHandle = open(self.logFile, 'a')
            self.logFileLock = threading.Lock()
    
        def WriteLine(self, logLine):
            self.logFileLock.acquire()
            output = self.TimeStamp() + '  ' + str(logLine) + '\n'
            self.fileHandle.write(output)
            self.logFileLock.release()
    
        def TimeStamp(self):
            stamp = time.strftime("%Y%m%d%H%M%S")
            return stamp


When an object is created it will create a text file with a timestamped name, this can then be written to by calling the WriteLine method. The thread locking happens within this object and means that the threads don't have to deal with it themselves. I'm unsure if this is actually the best way to do things but I've run a few tests and it works quite happily and feels elegant.

The quick testing script I used is below. All it does is create the logging object and then fire up a few threads which write stuff to the file in various functions. This is also my first try at using SyntaxHighlighter to make my code look half decent. May take a bit more tweaking to get it to work.

    
    #!/usr/bin/env python
    
    #Import Modules
    import os, threading, time
    
    class LoggingObj():
    
        def __init__(self):
            self.logFile = 'RenderServer-' + self.TimeStamp() + '.txt'
            self.fileHandle = open(self.logFile, 'a')
            self.logFileLock = threading.Lock()
    
        def WriteLine(self, logLine):
            self.logFileLock.acquire()
            output = self.TimeStamp() + '  ' + str(logLine) + '\n'
            self.fileHandle.write(output)
            self.logFileLock.release()
    
        def TimeStamp(self):
            stamp = time.strftime("%Y%m%d%H%M%S")
            return stamp
    
    class TestThread(threading.Thread):
    
        def __init__(self):
            self.blah = None
            threading.Thread.__init__(self)
    
        def run(self):
            self.TestSelf()
            LogFile.WriteLine(self.name + ': test thread running')
            self.AnotherTest()
    
        def TestSelf(self):
            time.sleep(1)
            LogFile.WriteLine(self.name + ': Initial test write')
    
        def AnotherTest(self):
            time.sleep(2)
            LogFile.WriteLine(self.name + ': Second test write')
    
    if __name__ == '__main__':
    
        global LogFile
    
        LogFile = LoggingObj()
    
        serverRunning = True
    
        LogFile.WriteLine('Cluster Server running')
    
        for threadNumber in range(4):
            newThread = TestThread()
            newThread.name = 'Test Thread ' + str(threadNumber)
            LogFile.WriteLine('Created ' + newThread.name)
            newThread.start()
