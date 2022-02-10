# Recent technical problems being worked on

## Urgent shutdown of all GCP resources

I had to perform network-intensive [GCP storage](https://cloud.google.com/storage/) operations, in order to completely shutdown a GCP project as quickly as possible, all motivated by keeping costs down to my credit card, ultimately completely disconnecting my credit card from the resources, b/c I got tired of paying for it.

There's an issue regarding the `gsutil rsync` command, and filenames with either _special characters_ or _brackets_ in them.  This is a long operation and you don't want the command to fail, but it did and does.  I had to narrow down which directories, in about 4 terabytes of data, to find/locate the files/folders which had erroneous filenames in them; then, I had to write and execute a brand new custom Python script using the official [google-cloud-storage](https://pypi.org/project/google-cloud-storage/) PyPi package to perform the download, and surely that succeeded.

This is the command:
```
gsutil -m -u project-id rsync -P -c -r gs://directory1 ./mnt/directory1
```

<!-- [the script I wrote](gcs_copy.py) -->
- https://stackoverflow.com/questions/54660013/how-to-download-folder-containing-brackets-in-name
- https://github.com/GoogleCloudPlatform/gsutil/issues/220
- https://cloud.google.com/storage/docs/gsutil/addlhelp/WildcardNames

## Failed laptop encrypted hard drive

_Linux Unified Key Setup, reading its source code, learning its commands, and running 'dd'_

I came home to find that my primary laptop's hard drive failed, and I had to just deal with it.  I had to learn and deal with the LUKS Linux encryption file system thing, not only having to discover/learn/run new commands (like `cryptsetup`, and `luksOpen`), but dealing with the source code itself **of** those command line tools.  All of the data was valuable, so I had to be careful, and so I had to know exactly what was going on, so dealing with these commands, and  their source code, was important to proceed with; thankfully the code was rather short.  I had to run the **dd if=/dev/sda of=/dev/sdb** command in attempts to at least perfectly mirror/backup the data, so that you can simply install Ubuntu back on it and the hard drive will be good as new, but I ran in to some errors with that command, and so now I'm stuck, and the laptop is just sitting here.  In the meantime it was fastest though to just use my older laptop for job hunting, and then get a job, and then get back to the issue.  Anyway, I usually use Ubuntu, and sometimes its using some transperant encryption thing underneath as the file system, and the point is is that it really is a transperant thing, meaning you're not supposed to really need to think about it.  But with this issue, it suddenly became **the** issue and one then has to dig under the hood and discover and learn about and deal with yet another new layer of software *stuff*.

## The Telly Fabric Project

Telly Fabric is the name of a web site that lets users create/operate/conduct virtual criminal/civil court cases.  The project also features a *simulation* component, which uses a separate asynchronous service which periodically sends text messages and emails to users - at the appropriate time - so that it lets the users really **feel**, in real time, the events portrayed in the court cases.  The intent is that it lets people create court cases and be lawyers or judges within those court cases without actually going to or dealing with a real/legal court.

- **High quality search functionality**.  This is very important, as the vast majority of the content is just text, and is always related to events in time, and you would want to search it.  [Whoosh](https://github.com/mchaput/whoosh) will be used.

- **Opinion measurement**.  Crucial to the system, is that all **opinions** about a court case can be measured.  Practically every court case in America has and makes *decisions* that are very very **fuzzy**; that is, the judge talks back and forth with the lawyers, and then when that's all over, they make some marks on exactly a single sheet of paper which **records the results** of all that discussion, and that's it; all you have is a single sheet of paper.  Telly Fabric measures and deals which *all* of the in-between stuff.

- **Strong internationalization language support**.  Lots of members of the public from different backgrounds, and that speak different languages, will need to use the system.  Django's support will be 100% used.

- Emphasis on **testing**.  There is lots of thoughts and opinions and facts and dependencies between them Lots of common folk people will need to use the system.  Use only Django's testing system.
