# Navigating Biomix

There are a few filesystems on Biomix that you should be familiar with.  These are `/home`, `/work`, and `/scratch`.  Below, I'll provide a brief summary of each and show you how to move between them.  In doing so, I will be discussing **directories**, **paths**, **variables**, and the commands `cd` and `ls`, but I will not be defining them.  If you are unfamiliar with these concepts, the beginning of the Bash/command line boot camp discusses them.  You do not need to go through the whole course to understand this lesson, just those concepts listed.

There is additional documentation on the filesystems [here](https://bioit.dbi.udel.edu/BIOMIX/BIOMIX-cluster.html#DiskSpace).

## Home

The most important location on Biomix is your **home directory**.  Upon logging in to Biomix, you are automatically placed in your home directory on the head node of the cluster.  Every Biomix user has their own home directory that is located at `/home/your_username`.  The path to your home directory can also be represented by the shorthand `~` and the variable represenatation is `HOME`.  If you type `echo $HOME` in to your command line on Biomix and hit enter, the output should be `/home/your_username`.  Home is a shared filesystem, so you will be able to access it from all Biomix nodes.

**`/home` is backed up regularly, and is the only filesystem on Biomix covered by backups.**  This makes it a good place to store some data, but keep in mind that home directories have storage limits (disk quotas) that are enforced.  

If you have data that is too big to be stored in your home directory but needs to be preserved and backed up, there is the option to lease additional storage.  Please contact help@bioinformatics.udel.edu for details.

## Work

`/work` can be used for temporary storage and to run jobs.  Like `/home`, `/work` is a shared filesystem that can be accessed from all nodes.  However, `/work` is NOT backed up and files will be deleted after 30 days of inactivity.  Jobs will generally run faster on `/work` than they would on `/home`, and there is no individual quota enforced, so `/work` is espcially ideal for running jobs that require large amounts of storage space (e.g., genome assemblies). 

You may need to create your own work directory.  To do this, use `cd /work` to move the `/work` filesystem.  To make your own directory, use `mkdir your_username`.  If you think you may already have a directory, include the `-p`- flag (`mkdir -p your_username`).  This version of the command will only create a new directory by that name if one does not already exist.  Note that while files that are more than 30 days old are automatically removed from `/work`, your directories may remain.

## Scratch

`/scratch` is another temporary workspace that is not backed up.  Unlike `/work` and `/home`, `/scratch` is a local filesystem that resides on individual nodes.  This means that if you create a file on Biomix 11, you will only be able to access it on Biomix 11.  The next lesson will teach you how to access a specific node.  

Like `/work`, computing jobs will run faster in a `/scratch` partition than in your home directory.  Because Biomix is heterogeneous, `/scratch` offers the benefit of providing a consistent environment/machine, which can be important for some tasks.

# Running jobs

In general, you should be using either `/work` or `/scratch` to run your slurm jobs, as this will be faster than using your home directory.  Additionally, many bioinformatics and computational biology jobs require greater storage capacity than exists in your home directory, and therefore must be performed elsewhere.  You will learn how to run jobs on Biomix in the next lesson.

For more information on these filesystems, including more detail on the differences between `/work` and `/scratch`, please see [this documentation](https://bioit.dbi.udel.edu/BIOMIX/BIOMIX-cluster.html#DiskSpace).

**Next lesson: [Biomix file systems](file_transfer_biomix.md).**

