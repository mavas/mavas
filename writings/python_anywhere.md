# PythonAnywhere.com deployment

Just recently learned about PythonAnywhere.com, that let's you host Django web sites for free; it's perfect, and has their own API at https://github.com/pythonanywhere/helper_scripts.

There were lots of little things that were different, but managable.  For example, they encourage you to use `mkvirtualenv` instead the more familiar `python -m venv venv` or `virtualenv env` usage.  You can only use the `SQLite3` database driver Django backend, and everything must be under 500MB in size, including both that database file and the search index directories.  It uses a familiar mechanism to securely pass environment variables, and aggressive `memcached` use should be effective.

I had to take 3 seperate Django `project` folders, and factor out the unique Django `app` in them, into [seperate Python packages](https://docs.djangoproject.com/en/4.0/intro/reusable-apps/), such that you can `pip install` them.  Then, it was easier to not only work in those 3 project folders seperately, but to also build a 4th Django web site for PythonAnywhere.com that incorporates the core of the other sites.

A good pipeline to develop is to make everything be entirely focused in the input and output of the http://XXX.pythonanywhere.com` web URL: two Whoosh search index directories need to be maintained, as well as an SQLite instance file, but so long as those 3 things are the sources and sinks of the pipeline, this can be a game changer.  You might integrate well with local docker container instances and images for development.

- 2 production whoosh index directories
- 1 SQLite production instance
- 1 local PostgreSQL instance docker container
- Heavily Django fixture oriented data (both whoosh indexes and all SQL
  databases)
