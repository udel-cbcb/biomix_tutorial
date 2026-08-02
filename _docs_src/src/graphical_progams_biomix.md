# Running graphical programs from Biomix

In addition to command line programs, you can also use Biomix for programs with a Graphical User Interface (GUI), like FastQC or MATLAB.  For this, you may need to do a bit of configuration on your own computer.  As always, please **be careful about what you are running on the head node**.  Graphical applications, especially computing GUIs like MATLAB, can be computationally expensive and launching them from the head node may slow down Biomix and interrupt others' work.

## Setup

Even though you will be using Biomix to run the software, your own computer will need a windowing system to display the graphical aspect of the program.  Specifically, you will need to use a method called X11 forwarding, which is an `ssh` feature that allows you to run graphical programs from a remote server using your local machine's X server

To do this, your PC will need to be equipped with a windowing system.  We recommend [XQuartz](https://www.xquartz.org/) for MacOS and [Xming](https://sourceforge.net/projects/xming/) for Windows.  Most Linux distributions come with X11 forwarding by default.

Follow the link for your operating system above, download the latest version of the software, then follow your system instructions to install.  Then, it is highly recommended that you restart your cmputer so that the changes implemented by the software can take effect.

## Launching a program

For this example, we are going to launch xeyes, a fun little program that pops up a set of eyes that watch your mouse move around the screen.  Because there is a graphical component (the eye animation), it's a great way to test if your window forwarding is working.

*A quick note, we have noticed that WSL can be difficult to configure for X11 forwarding.  If you are using WSL to connect to Biomix and run into issues, we recommend switching to PuTTY for this purpose.*

1\. First, log in to Biomix with X11 forwarding enabled:

* PuTTY users: Open PuTTY.  In the menu on the left-hand side, expand the `ssh` settings by hitting the `+` button next to "SSH."  Then, click on "X11."  In the menu that appears, make sure that the box labeled "Enable X11 forwarding" is checked.  Then, log in to Biomix as usual.

* Everyone else: Open a terminal window on your local machine and connect to the remote Linux server using `ssh` with X11 forwarding enabled by running the following command:

        ```{bash}
        ssh -X username@biomix.dbi.udel.edu
        ```

If you encounter an error using this command, try using the `-Y` instead of `-X`.  `-Y` enables trusted X11 forwarding, which is safe to use here because Biomix is a trsuted server

2\. Once you are connected to Biomix, submit an interactive Slurm job to allocate resources for running RStudio. To do this, run the following command:

```{bash}
srun --x11 --mem=2000  --pty bash 
```

This will allocate 2GB of memory and for your interactive Slurm job, and launch a Bash shell in your job.  Depending on what program you are launching and what you are doing, you may need more or less time or memory. 

The `--x11` option enables X11 forwarding within the job, which is what will launch the GUI.

3\. Once your interactive Slurm job has started, you should see a new prompt in your terminal window. From this prompt, launch xeyes by running the following command:

```{bash}
xeyes
```

A pair of googly eyes should now appear on your local screen, displayed through X11 forwarding.  They should follow your mouse as you move it around the screen.

4\. When you are done using your graphical program, close the window.  If this does not stop the process running on Biomix, use `^C` to terminate it.  Don't forget to exit the interactive job and logout of Biomix, if you are finished.
