## Urgent shutdown of all cloud resources

I had to perform network-intensive [GCP storage](https://cloud.google.com/storage/) operations, in order to completely shutdown a GCP project as quickly as possible, all motivated by keeping costs down to my credit card, ultimately completely disconnecting my credit card from the resources, b/c I got tired of paying for it.

There's an issue regarding the `gsutil rsync` command, and filenames with either _special characters_ or _brackets_ in them.  This is a long operation and you don't want the command to fail, but it did and does.  I had to narrow down which directories, in about 4 terabytes of data, to find/locate the files/folders which had erroneous filenames in them; then, I had to write and execute a brand new custom Python script using the official [google-cloud-storage](https://pypi.org/project/google-cloud-storage/) PyPi package to perform the download, and surely that succeeded.

This is the command:
```
gsutil -m -u project-id rsync -P -c -r gs://directory1 ./mnt/directory1
```

This of course isn't just ME - other people on the Internet have ran into the same issue, and it's still a pressing issue.  Here are some links about this problem.  The solution is to write a custom Python script to do the same thing as what the `gsutil` command does.

<!-- [the script I wrote](gcs_copy.py) -->
- https://stackoverflow.com/questions/54660013/how-to-download-folder-containing-brackets-in-name
- https://github.com/GoogleCloudPlatform/gsutil/issues/220
- https://cloud.google.com/storage/docs/gsutil/addlhelp/WildcardNames
