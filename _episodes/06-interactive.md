---
title: "Running an interactive job on M2"
teaching: 15
exercises: 0
questions:
- "How do I request and interact with a compute node?"
objectives:
- "`srun`, `modules`"
keypoints:
- "`srun` sends a request for a compute node to the scheduler"
- "software available on M2 is organized into modules according to version"
- "modules need to be loaded before use"
---

Now, we arrive at the most important part of today's workshop: getting on the compute nodes. Compute nodes are the real power of M2. Let's see which of the compute nodes are available at the moment:

~~~
cat /hpc/motd/m2_queue_status 
~~~
{: .bash}

We can see that the cluster is quite busy, but there is a fair amount of compute nodes that are available for us. Now, let's request one compute node. Please type the following (or paste from the website into your SSH terminal):

~~~
srun -p standard-mem-s -n 1 -c 10 --mem=16G --pty $SHELL
~~~
{: .bash}

It is very important not to make typos, use spaces and upper/lowercases exactly as shown, and use the proper punctuation. If you make a mistake, nothing wrong will happen, but the scheduler won't understand your request.

Now, let's carefully go through the request:

- `srun` means that we are asking the SLURM scheduler to grant us access to a compute node;
- `-p standard-mem-s` means it's an partition targeting to queue standard-mem-s
- `-n 1` means we are asking for one compute node;
- `-c 10` means that we only need ten CPUs on the node 
- `--mem=16G` means that we are asking for 16 Gb of RAM.
- `--pty $SHELL` means that you are requesting to run in an Interactive node

This is actually a very modest request, and the scheduler should grant it right away. Sometimes, when we are asking for much substantial amount of resources (for example, 20 nodes with 40 cores and 370 Gb of RAM), the scheduler cannot satisfy our request, and will put us into the queue so we will have to wait until the node becomes available. 

Once the request is granted, you will see something like that:

~~~
srun: job 25719448 queued and waiting for resources
[tuev@b123 ~]$
~~~
{: .output}

Please note two important things. First, our prompt changes from `login01` to `b123` which is the compute node name.

In order to see how many jobs that you are running:

~~~
squeue -u your_username
~~~
{: .bash}

~~~
$ squeue -u tuev
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
          25717171   gpgpu-1 sys/dash     tuev  R 2-20:46:59      1 p027
          25713508 standard- sys/dash     tuev  R 2-23:03:18      1 b123
~~~

You can see in the above command, I have 2 running jobs (StaTus="R") with JobID, Partition, number of nodes and nodes' name.

To exit the compute node when inside, type:

~~~
exit
~~~

{: .bash}

This will bring you back to the login node. See how your prompt has changed to `login01`. It is important to notice that you have to be on a login node to request a compute node. One you are on the compute node, and you want to request another compute node, you have to exit first, else you will have error similar to this:

```
srun: error: Unable to allocate resources: Access/permission denied
```

For some jobs, you might want to get a GPU, or perhaps two GPUs. For such requests, the `srun` command needs to specify the number of GPUs (one or two) and the queue of GPUs. For example, let's request a NVIDIA Tesla P100 

~~~
srun -p gpgpu-1 --gres=gpu:1 -n 1 -c 10 --mem=25G -t 1-00:00:0 --pty $SHELL
~~~
{: .bash}

Here we asked the scheduler to allocate 1 node with 25G memory in partition gpgpu-1 (the partition with P100 GPU) and asked for 1 GPU for that node (--gres=gpu:1) with the walltime of 1 hour.

If the scheduler receives a request it cannot satisfy, it will complain and not assign you to a compute node (you will stay on the login node). For example, if you ask for a node with 2.5TB of memory.

It is possible to ask for several compute nodes at a time, for example `-n 4` will give you 4 compute nodes. This will give you more nodes to run your parallel jobs.

It is very important to remember that you shouldn't run computations on the login node, because the login node is shared between everyone who logs into m2, so your computations will interfere with other people's login processes. However, once you are on a compute node, you can run some computations, because each user gets their own CPUs and RAM so there is no interference. If you are on the login node, let's get on the compute node:

We have a lot of software installed on M2, but most of it is organized into *modules*, which need to be loaded. For example, we have many versions of Matlab installed on M2, but if you type

~~~
matlab
~~~
{: .bash}

you will get an error:
~~~
-bash: matlab: command not found
~~~
{: .error}

In order to use Matlab, as well as most other software installed on Palmetto, you need to load the Matlab module. To see which modules are available on M2, please type

~~~
module avail
~~~
{: .bash}

If you want to see which versions of Matlab are installed, you can type

~~~
module avail matlab
~~~
{: .bash}

~~~
------------------------------------------------------------------------------------------- /hpc/modules/applications -------------------------------------------------------------------------------------------
   matlab/r2016b    matlab/r2017a    matlab/r2018b    matlab/r2020b    matlab/r2021a    matlab/r2021b (D)

  Where:
   D:  Default Module

Module defaults are chosen based on Find First Rules due to Name/Version/Version modules found in the module tree.
See https://lmod.readthedocs.io/en/latest/060_locating.html for details.

Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".

~~~
{: .output}

Let's say you want to use Matlab 2020. To load the module, you will need to specify its full name:

~~~
module load matlab/r2020b
~~~
{: .bash}

To see the list of modules currently loaded, you can type

~~~
module list
~~~
{: .bash}

If the Matlab module was loaded correctly, you should see it in the module list. In order to start command-line Matlab, you can type

~~~
matlab
~~~
{: .bash}

To exit Matlab, please type `exit`. To unload a module, you an use `module unload matlab/r2020b` command. To unload all the modules, please type

~~~
module purge
~~~
{: .bash}

Now, if you do `module list`, the list should be empty. Now, let's start R. To see which versions of R are available, type

~~~
module avail r
~~~
{: .bash}

This will give you a list of all modules which have the letter "r" in them (`module avail` is not very sophisticated). Let's see what happens when you load the R 4.0.2 module:

~~~
module load r/4.0.2
module list
~~~
{: .bash}

~~~
Currently Loaded Modules:
  module list

Currently Loaded Modules:
  1) spack                              10) xz-5.2.4-gcc-9.2.0-s2pq3zl           19) gdbm-1.18.1-gcc-9.2.0-kbpmprj          28) libpthread-stubs-0.4-gcc-9.2.0-npwz2jl  37) libxrender-0.9.10-gcc-9.2.0-sh65nie
  2) texlive/2017                       11) libxml2-2.9.9-gcc-9.2.0-bumngif      20) perl-5.30.0-gcc-9.2.0-y34vqqu          29) xproto-7.0.31-gcc-9.2.0-cvg2oci         38) pixman-0.38.0-gcc-9.2.0-hfbzyac
  3) intel-2020.0                       12) fontconfig-2.12.3-gcc-9.2.0-ppslo43  21) libbsd-0.9.1-gcc-9.2.0-amtukbv         30) libxau-1.0.8-gcc-9.2.0-yvbglct          39) cairo-1.16.0-gcc-9.2.0-77dxsgb
  4) font-util-1.3.2-gcc-9.2.0-36ydpw2  13) ncurses-6.1-gcc-9.2.0-cujtgm6        22) expat-2.2.9-gcc-9.2.0-vf36ozs          31) libxdmcp-1.1.2-gcc-9.2.0-bpnbnhc        40) curl-7.63.0-gcc-9.2.0-n4hxp7l
  5) bzip2-1.0.8-gcc-9.2.0-tcftk7k      14) tar-1.32-gcc-9.2.0-zc2tgas           23) openssl-1.0.2k-fips-gcc-4.8.5-wmsz3ya  32) libxcb-1.13-gcc-9.2.0-koebrst           41) icu4c-64.1-gcc-9.2.0-cdj6hu7
  6) zlib-1.2.11-gcc-9.2.0-62irkl4      15) gettext-0.20.1-gcc-9.2.0-xpdiisw     24) sqlite-3.30.1-gcc-9.2.0-jhc7qek        33) xextproto-7.3.0-gcc-9.2.0-c5lnetz       42) jags-4.3.0-gcc-9.2.0-lkql3wp
  7) libpng-1.6.37-gcc-9.2.0-74mkb2u    16) libffi-3.2.1-gcc-9.2.0-vve5ph3       25) python-3.7.4-gcc-9.2.0-3zfxo7j         34) libx11-1.6.7-gcc-9.2.0-ftn75aa          43) gdal-3.2.0-gcc-9.2.0-z36d74a
  8) freetype-2.10.1-gcc-9.2.0-bpqzywe  17) pcre-8.42-gcc-9.2.0-7ac4une          26) glib-2.56.3-gcc-9.2.0-a6ugasf          35) libxext-1.3.3-gcc-9.2.0-kacb3uk         44) r/4.0.2
  9) libiconv-1.16-gcc-9.2.0-repeu56    18) readline-8.0-gcc-9.2.0-qoxthhf       27) kbproto-1.0.7-gcc-9.2.0-nk4nrm7        36) renderproto-0.11.1-gcc-9.2.0-xcsjaeg


~~~
{: .output}

R depends on other software to run, so we have configured the R module in a way that when you load it, it automatically loads other modules that it depends on.

