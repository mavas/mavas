# Things I've done with Google Cloud

- Django on AppEngine, along with Cloud SQL istance.  This is a great setup, as the only thing you care about is 1.) that Django folder, and 2.) using a single command to deploy __from__ that directory: ~~~gcloud app deploy~~~.

- Terabytes of data in Google Cloud Storage (GCS).  I've used **gsutil** many times, mostly **gsutil rsync**.  I've used the **google-cloud-storage** Python PyPi package many times to do things programatically.  You can use it along with the Django+AppEngine+CloudSQL setup above to serve static files for web production.  I was about to use Apache Beam to do some huge data processing, following [this](https://www.tensorflow.org/datasets/beam_datasets) guide, but couldn't in time.

- You can use your own Docker containers and deploy them to CPU instances and do custom things.  For example, I had to deal with the **scrapyd** Twisted server, and deploy it as a server, on a CPU, in the cloud, and you can do that with containers.  I successfully got the **google-cloud-logging** module to log to StackDriver Logging, just using standard Python logging module calls.  The scrapyd program is just Python, and thankfully the image that was used for it was "FROM: Python3.8".

- Cloud SQL instances have been created for both development and production, mostly because Django installations require a running SQL server of some kind.  Thankfully Cloud SQL supports PostgreSQL.  Integration between a Cloud SQL instance and Django-on-AppEngine instances is seemless, oftentimes just DEFINING and ADDING an additional setting in you standard Django settings.py file, saying whether this is AppEngine or not.
