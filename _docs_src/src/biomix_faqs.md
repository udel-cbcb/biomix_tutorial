# Biomix Frequently Asked Questions (FAQs)

## About Biomix

### Who can use Biomix?

Biomix is available to life science researchers throughout Delaware.  You do not have to be affiliated with UD to use Biomix.  

### How do I get a Biomix account?

To get an account, please email the DBI-IT team at dbi-it@udel.edu.  Please be sure to indicate your role (e.g., faculty, student, etc.) and what institution you are from.  If you are a student researcher, post-doc, or other member of a research lab make sure to include the name of your PI. 

### Where can I find documentation and tutorials for Biomix?

Biomix documentation and tutorials can be found on The [Bioinformatics Core facility training page](https://bioinformatics.udel.edu/core/training/).

### Is there a charge for using Biomix?

Biomix and other computational resources offered by the Core are made available free-of-charge through the support of Delaware INBRE (NIH P20 GM103446) and the State of Delaware. Please acknowledge this contribution in any publications resulting from their use.

### How do I cite Biomix?

The personnel and computational infrastructure of the CBCB Bioinformatics Core and Delaware Biotechnology Institute are supported by a number of grants and other sources which significantly defray costs to our clients. To maintain these sources of support, it is critical that any publications or other products supported by our Core Personnel or using BIOMIX and other bioinformatics infrastructure of the core, include a statement of acknowledgement similar to the following:

*“Support from the University of Delaware Center for Bioinformatics and Computational Biology Core Facility and use of the BIOMIX compute cluster was made possible through funding from Delaware INBRE (NIGMS P20GM103446), the State of Delaware, and the Delaware Biotechnology Institute.”*

## Technical questions

### How much storage is available on Biomix?

Individual users are allotted TODO GB of storage in their home directories.  There are other locations on Biomix where large files may be stored temporarily, but home directories are the only locations on Biomix that are backed up regularly.

### What if I need more storage?

A number of the Biomix compute nodes were purchased by users to support their research, including for the purpose of providing additional storage. We can help you select, purchase, and maintain your machine, and even connect it to Biomix.  

If you are looking to store biomedical data, you may be eligible to use [Biostore](https://bioinformatics.udel.edu/Core/DataCenter/), a high performance Dell Isilon Storage Cluster with >3PB of storage.

Inquire about both of these options by sending an email to help@bioinformatics.udel.edu.

## What does it mean to put something to my path?

This is covered in the section "Path variables" in the lesson [Running software on Biomix](running_software_biomix.md).

## Common errors

Please see our [troubleshooting guide](troubleshooting_guide.md) for guidelines and tips for successful troubleshooting, especially for errors not explicitly addressed in the FAQs.

### Issues connecting to Biomix

#### Cannot connect to server or similar

`ssh: connect to host biomix.dbi.udel.edu port 22: Operation timed out`

`ssh: connect to host biomix.dbi.udel.edu port 22: Connection refused`

There are multiple causes and solutions for these errors, which occur immediately upon attempting to connect to Biomix without prompting you for your password.  

Usually the above errors indicate that your IP address has been blocked on Biomix.  Here are the most likely causes and their solutions: 

1. The most likely cause is entering your password or username incorrectly multiple times in a row, which will cause Biomix to put a block on your IP address.  To reconnect, you will either need to wait a few hours (no more than 24) after your last incorrect password/username entry or contact DBI-IT (dbi-it@udel.edu) to remove the block.  When you are no longer blocked, be careful to enter your password/username correctly; watch out for capital letters and symbols that look similar (e.g., `O/0`, `l/I/1`).

2. Another possibility is that your IP address was blocked by a routine security scan.  This is likely the case if you are receiving one of the above messages without having any recent failed login attempts.  As a test, you can try to connect to Biomix using another network (e.g., cellular, network at UD, [UD's VPN](https://services.udel.edu/TDClient/32/Portal/KB/ArticleDet?ID=113)).  This issue will not be resovled by waiting for a few hours, so you will need to send DBI-IT (dbi-it@udel.edu) an email with your **IPv4** address, which you can get by using [this website](https://www.whatismyip.com).  The DBI-IT team will either remove the block or inform you that an IP block is not the issue. 

If the connection issue does not stem from an IP block, there are other rare explanations.  

1. The first is that your internet service provider (ISP) is blocking ssh connections, which would impede your access to Biomix.  Using another network, such as the VPN should get around this issue, but you can also contact your ISP for help.  

2. The second possibility is that your connection is being blocked by a firewall.  This is unlikely to be the issue if you have been able to connect to Biomix in the past from the same computer, but can occur after system updates.  To fix this, you will need to look up solutions specific to your operating system.  You should be able to do so using Google and "firewall blocking ssh [OS]" or a similar phrase, inserting your own operating system in place of [OS].

#### Broken pipe

`client_loop: send disconnect: Broken pipe`

This message means that your connection to Biomix has been lost.  There are a number of possible causes, but the two most common are allowing your computer to go to sleep and an unstable internet connection.  

You can test the stability of your internet connection using [this website](https://ping.canbeuseful.com/en).  One fix is to use an ethernet connection rather than wifi.  If you are at home, you may also try resetting your router.  If resetting the router and using ethernet do not fix the problem, you may need to contact your service provider.

### Linux errors

When troubleshooting Linux errors, the most important thing to remember is that Biomix is not wrong.   If Biomix is giving you an error or an unintended result, it means that you have given it instructions that it does not fully understand.  

#### No such file or directory

This is a very common error when working on a Linux system and can be frustrating to solve.  The error is always a result of the computer being unable to find a file or directory based on your instructions.  The most common causes are:

* A file or directory name is misspelled
* The path to the file or directory is inaccurate (especially likely if providing relative paths)

Useful techniques and commands for resolving the error:

* Use tab completion or copy and paste file paths and names to avoid misspellings
* Use the command `pwd` to make sure you are located where you think you are
* Use the `realpath` command to make sure that the path to the file or directory is accurate
* Use an absolute path rather than a relative one (e.g., `~/results/results.txt` rather than `../results/results.txt`)

#### Command not found

This error appears if Biomix does not recognize the command you are trying to run.  The most common causes are:

* No command was provided 
* The command is misspelled
* The command is not on the user's path
* The user is trying to run an executable file without providing `./` before the file name

# Asking for help

Questions about Biomix may be directed to dbi-it@udel.edu (reaches only the IT team) or help@bioinformatics.udel.edu (reaches the DBI IT team plus the [Bioinformatics Data Science Core Facility staff](https://bioinformatics.udel.edu/core/bioinformatics-experts/))
