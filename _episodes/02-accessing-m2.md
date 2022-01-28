---
title: "Accessing the M2 Cluster"
teaching: 15
exercises: 0
questions:
- "How can I access the M2 cluster from my local machine?"
objectives:
- SSH client, Terminal, MobaXTerm, Open OnDemand
keypoints:
- "M2 can be accessed by an SSh (secure shell) client"
- "Windows user can use `MobaXTerm` application"
- "Mac users can use the `Terminal` application"
- "Open OnDemand platform"
---

M2 is accessed using the SSH (["Secure shell"](https://en.wikipedia.org/wiki/Ssh_(Secure_Shell))) protocol.M2 runs the *SSH server*; on your local machine, you will need to run *SSH client* which connects to a server using a command-line *terminal*. The commands that are entered on the terminal are processed by the server on M2.

To start the SSH client on a Mac, you can open the Terminal Application (which is usually located in `Applications` &rarr; `Utilities`) and run the following:

~~~
ssh your_username@m2.smu.edu
~~~
{: .bash}

For Windows, first you need to download and install
[MobaXterm Home Edition](https://mobaxterm.mobatek.net/download.html).

> It is important that you unzip the downloaded installer prior to installation.
> The zipped installer file contains an additional data file besides the installer
> executable. This data file is not accessible if the installer executable is
> called from inside the zipped file (something Windows allows you to do).
{: .callout}

After MobaXterm starts, click the `Session` button.

<img src="../fig/mobaxterm_0.png" alt="Main MobaXterm Windows" style="height:350px">


Select SSH session and use the following parameters (whichever required), then click `OK`:

* Remote host: `m2.smu.edu`
* SSH-browser type: Enhanced SCP
* Port: 22

![image](https://user-images.githubusercontent.com/43855029/151621177-eeb100d7-1371-460f-b421-45fe6d9cb4aa.png)

At this stage, for both Mac and Windows, you will be asked to enter your username
and password, then DUO option.
**Note**: when typing in password, due to security, you won't see anything on the screen. So make sure you type the password correctly.

![image](https://user-images.githubusercontent.com/43855029/151621297-73ad463d-6be3-4957-af3e-2a33729654fa.png)

When logged in, you are presented with a welcome message and the following "prompt":

~~~
[username@login01 ~]$
~~~

{: .bash}

The prompt in a bash shell usually contains a (`$`) sign, and shows that the shell is waiting for input. The prompt may also contain other information:
this prompt tells you `your username` and which node you are connected to - `login01` is the "login" node. (There are total 5 login nodes on M2)

It also tells you your current directory, i.e., `~`, which, as you will learn shortly, is short for your *home* directory.

In the figure below, MobaXterm also gives you a GUI browser of your home directory on M2. For Mac OS and Linux terminal, you will only have the
command line interface to the right.

![image](https://user-images.githubusercontent.com/43855029/151621618-9c2b8bfe-7a7e-48ad-843e-5ffde2869912.png)
