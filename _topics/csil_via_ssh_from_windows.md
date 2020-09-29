---
topic: "CSIL: via ssh from Windows"
desc: "Connecting via PuTTY/XMing or MobaXterm"
indent: true
---

To connect to the CSIL machines from Windows, you need a piece of software known as an *ssh client*

# Goodbye PuTTY/XMing, Hello MobaXTerm

The most commonly used ssh client in the past has been a program called PuTTY.

PuTTY works fine for any program that doesn't use graphics.  However, to access the graphics capabilities of the 
CSIL machines, you also need a piece of software known as an *X11 server*, such as XMing.

Configuring PuTTY and XMing to work together can be tedious.   Why bother, when there is now a free program that
combines both, called MobaXTerm.

You can download MobaXterm from this link: [http://mobaxterm.mobatek.net/](http://mobaxterm.mobatek.net/)

# How to use MobaXTerm to connect to CSIL

Once you have downloaded it, you want to use it to create a new session.  The [demo shown at this link](http://mobaxterm.mobatek.net/demo.html) pretty much illustrates the process.  

* Click "new session"
* Select "ssh"
* For "remote host", instead of `192.168.56.86` you'll enter `csil.cs.ucsb.edu` 
  * NOTE: Yes, `csil.cs.ucsb.edu` for Fall 2020, not `csil-01.cs.ucsb.edu` through  `csil-48.cs.ucsb.edu`.  That's new for Fall 2020.
* For "username", instead of `root`, you'll enter your CSIL username.
* The first time you connect to a particular system, you may be asked 
* It should then prompt you for your password.  (I do not recommend "saving the password".)

# SSH Port Forwarding

*When you want to access a `localhost:8080` web app running on CSIL from a non-CSIL computer, e.g. your laptop*

At a command prompt (terminal prompt on MacOS, Linux, WSL, Windows 10, or git bash shell on Windows), you can type this:

`ssh -L 8080:localhost:8080 username@csil.cs.ucsb.edu`

where:
* `username` is your actual CSIL username

That will set up port 8080 on your local machine as a tunnel to "localhost:8080" on the CSIL machine.    Then, if you put `localhost:8080` in your browser, you should be getting access to `localhost:8080` on the CSIL machine you are ssh'ing into.

NOTE HOWEVER, that only one user at a time can be using port 8080 on the CSIL side.  So, if you port 8080 isn't available on the CSIL side, you may need to use a different port number.  Be aware that if you are using OAuth authentication, the port number may be baked into the OAuth credentials, so you might have to make changes to your OAuth config if you use a different port.

