# Recent technical problems being worked on

## Failed laptop encrypted hard drive

_Linux Unified Key Setup, and its source code_

I came home to find that my primary laptop's hard drive failed, and I had to just deal with it.  I head to learn and deal with the Luks Linux encryption file system thing, not only running commands (like 'luksOpen'), but dealing with the source code itself **of** those command line tools, just know exactly what was going on.  All of the laptop data was valuable, so I had to be careful, and so dealing with these commands, and  their source code, was important to proceed with.  I had to run the "dd if=/dev/sda of=/dev/sdb" command in attempts to at least perfectly mimorro/backup the data, so that you can isimply install Ubuntu back on it and the hard drive will be good as new, but I ran in to some errors with that command, and so now I'm stuck, and the laptop is just sitting here.  In the meantime itwasfastest though to simply use my older laptop for job hunting, and hten get a job, and then get back to the issue.  I h

## Urgent shutdown of all GCP resources

Perform network-intensive GCP storage operations, in order to completely shutdown a GCP project as quickly as possible, all motivated by keeping costs down to my credit card, ultimately completely disconnecting my credit card with the resources, b/c I got tired of paying for it.

There's an issue regarding the gsutil rsync command and filenames with either special characters or brackets in them.  This is a long operation and you don't want the command to fail, but it did.  I had to narrow down which directories, in about 4 terabytes of data, to find/locate the folders which had erroneous filenames in them, and had to write and execute a brand new custom Python script using the official google-cloud-storage PyPi package to perform the download, and surely that succeeded.  https://github.com/GoogleCloudPlatform/gsutil/issues/220, https://cloud.google.com/storage/docs/gsutil/addlhelp/WildcardNames, https://stackoverflow.com/questions/54660013/how-to-download-folder-containing-brackets-in-name .

> # The command I ran that got errors regarding the copy of certain files..
> gsutil -m -u project-id rsync -P -c -r gs://directory1 ./mnt/directory1

[the script I wrote](gcs_copy.py)
