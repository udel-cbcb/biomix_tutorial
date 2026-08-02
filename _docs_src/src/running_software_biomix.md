# Using software on Biomix

*Note: This lesson covers running command line programs.  If you are interested in using Biomix to launch a program with a graphical user interface (GUI), such as MATLAB or RStudio, please see the instructions in the lesson ["Running graphical programs on Biomix"](graphical_progams_biomix.md).*

## Running software

Many of the most frequently used bioinformatics and computational biology programs are already installed on Biomix (complete list [here](https://bioit.dbi.udel.edu/BIOMIX/BIOMIX-software.html)).  The instructions for enabling your account to run software are going to vary, but will be listed either on the Biomix software page or in the software's documentation.  We will be referring to the Biomix software page frequently, so make sure to have it open.

Some programs will run without any preparation.  Take Clustal Omega for example.  If you are logged in to Biomix, you should be able to run the command `clustalo --help` and see the command line help documentation print to the screen.

Some programs require that you add them to your **path variable**.  One example is RAxML, a phylogenetic tree builder.  Before you can run RAxML, you will need to run the command `PATH=$PATH:/usr/local/DAS_Tool` to include it on your path.  If you are not familiar with any of the concepts in this paragraph, please skip down to the section called "Path variables" for more information.

A handful of programs, like SRA (Sequence Read Archive) Toolkit, need to be enabled using the `source` command.  To use the Toolkit, you will need to run `source /usr/local/ncbi/sra-tools.sh` each time you want to use it in a new session. While a directory will stay in your path variable unless removed, a sourced script will only remain available during the same log in session.  To demonstrate, try to run `sra-search`.  You should get a `command not found` error from bash.  Now, run `source /usr/local/ncbi/sra-tools.sh` and then run `sra-search` again.  This time, you get an error from the program itself for not including arguments and a small help section.  Next, log out of Biomix and log back in.  If you try to run `sra-search` a third time, you should get that first bash `command not found` error.

Additionally, many of the software on Biomix are python-based and rely on `conda` environments.  These programs are not indicated on the website, so you will need to visit the software documentation for this information and usage instructions.  You can read more about conda [here](https://docs.conda.io/en/latest/) and conda environments [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).  Conda is already available on Biomix, so there is no need to install it.

### Path variables

Some programs require that you add them to your **path variable**.  The path variable stores a list of directories where **executable** files are located.  Executable files, or executable programs, are what actually cause a program/software to run.  In other words, they contain instructions that, when activated, tell a computer what to do and how to run a program.  You can view your path variable the same way you view any other Linux variable:

```{bash}
[aoh@biomix ~]$ echo $PATH
/usr/local/bcftools/bin:/home/aoh/.rbenv/shims:/home/aoh/.rbenv/shims:/home/aoh/.cargo/bin:/home/aoh/miniconda3/condabin:/usr/lib64/mpich/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/aoh/.rbenv/bin:/home/aoh/bin:/usr/lib64/qt-3.3/bin:/usr/lib64/mpich2/bin:/usr/lib64/ccache:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/c3-5/:/usr/local/samtools-0.1.18:/home/aoh/software/standard-RAxML-8.2.8/:/home/aoh/scripts:/home/aoh/software/color_tree-0.7.0-alpha/:/home/aoh/.rbenv/bin:/home/aoh/.rbenv/shims:/home/aoh/.cargo/bin:/home/aoh/miniconda3/condabin:/usr/lib64/mpich/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/aoh/.rbenv/bin:/home/aoh/bin:/usr/lib64/qt-3.3/bin:/usr/lib64/mpich2/bin:/usr/lib64/ccache:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/opt/c3-5/:/usr/local/blast-2.2.22/bin/:/usr/local/samtools-0.1.18:/home/aoh/software/standard-RAxML-8.2.8/:/home/aoh/scripts:/home/aoh/software/color_tree-0.7.0-alpha/:/home/aoh/.rbenv/bin:/usr/local/AMOS/bin:/usr/local/MUMmer3.23:/usr/local/AMOS
```

As previously stated, this is a list of directories that each contain executable files, where individual paths are separated by colons.  So, `/usr/local/bcftools/bin` is one directory that contains an executable, and `/home/aoh/.rbenv/shims` is another.  Note that your path variable is likely to be much shorter than the one above; the example is a portion of the path variable from a long-time and frequent user of Biomix.

Now that you know what a path variable *is*, you may be wondering what it's *for*.  Path variables are useful because they allow you to call programs without providing full paths.  Essentially, it's a shortcut.  Let's look at Clustal Omega as an example again.  One way to find out where an executable file is located is to simply ask it.  If you run `which clustalo`, you should get the output `/usr/bin/clustalo`.  This tells you that the executable for Clustal Omega is located in `/usr/bin`.  In fact, go ahead and list out that directory using the command `ls /usr/bin`.  You should see an executable called `clustalo` listed as one of the contents of the directory.  Now, try running `/usr/bin/clustalo --help`.  This should produce the same result you saw previously in this lesson.

And this is also applies to most of the Linux and Slurm commands you have been running as well.  If you list out the contents of `/usr/bin`, you will see the executables for `grep`, `scancel`, and even `ls` listed among the many files.  In fact, you can get a little meta and run `/usr/bin/ls /usr/bin` to list the contents of the directory that contains `ls`.

At this point, hopefully, you are wondering what is happening behind the scenes to make all of this work.  Each time that you try to run a command, Bash starts looking for its executable.  And where does it look?  In all of those directories in the path variable.  If it finds the executable in one of those directories, then the command gets run.  If not, bash throws a `command not found` error.  

Now, that you have an idea of how this all works, let's look at a couple of commands, starting with the one for RAxML.  To put RAxML on your path, you would need to run `PATH=$PATH:/usr/local/DAS_Tool`.  This command simply re-assigns the `PATH` variable to be itself, followed by `:/usr/local/DAS_Tool`.  **If you add a directory to your path this way, it will stay there until it is manually removed.**

Another flavor of this re-assignment uses the `export` command.  You can see this in the instructions for running Xenium Ranger, part of the Xenium In Situ software suite for gene expression data.  To use Xenium Ranger, you first need to run `export PATH=/usr/local/xeniumranger-xenium4.0:$PATH`.  Running that command followed by `echo $PATH` would show a new directory at the beginning of your path variable, `/usr/local/xeniumranger-xenium4.0`.  You would now be free to run Xenium Ranger without providing the full path to the software in your command.  However, if you were to log out of Biomix and then log back in, running `echo $PATH` would show `/usr/local/xeniumranger-xenium4.0` to  have vanished from your path!  And if you try to run Xenium Ranger, you will get a pesky `command not found` error.  So, **using export to add a directory to your path is temporary, and the directory will only stay in your path for that session**.  

TODO: any practical reasons for picking one of these two methods for software?  other than not wanting to clutter up the path?  

One last important thing to note is that **the order of directories on your path matters**.  Let's say, for example, that you need to use a different version of a made-up program called SnazzyAnalyzer (version 2), than is already installed on Biomix (version 3) to replicate an experiment.  You install the version of the software that you need and add it to the end of your path (in this example, it does not matter if you use `export` or not).  However, when you run the command `snazzy -v` to get the version number, you get back the number of the version that was already on Biomix, not the version that you just installed.  You decide to look at your path and see this:

```{bash}
[aoh@biomix ~]$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/username/snazzy-3/snazzy:/home/username/snazzy-2/snazzy
```

**When bash looks through directories to find executables, it looks through them in the order that they appear on your path**.  That means that when you run `snazzy -v`, bash finds the `snazzy` command from the SnazzyAnalyzer v3 before if finds the version from the SnazzyAnalyzer v2.  To remedy this, you would either need to remove version 3 from your path, or run version 2 using the whole path like this, `/home/username/snazzy-2/snazzy -v`.

# Next steps

This marks the end of the beginner Biomix tutorial.  You're now ready to roll for almost everything that a typical Biomix user needs to accomplish!  For other topics, including tips on installing software on Biomix, see the "Expanded Topics" section.  We have also put together some [Frequently Asked Questions](biomix_faqs.md) and a [Trouble Guide](troubleshooting_guide.md) to help you fulfill your Biomix dreams.
