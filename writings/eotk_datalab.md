# EOTK and Datalab containers

- github.com/alecmuffett/eotk/opt.d/build-ubuntu-20.04.sh

## Reading the datalab source code

I don't remember being required to dive into the code of Google Cloud's [Datalab](https://github.com/googledatalab/datalab), but I did anyway and was impressed by how it was built.  It really shows what someone could do if they have a **wide** variety of experience, because this project definitely took into account, and integrated, a number of various technologies, to produce a new and clean product: bash scripting, Docker, NodeJS, web development, and security.

The project is somewhat obsolete now, with the new [JupyterLab](https://jupyter.org/) project being the next generation of Datalab, but it was still good to look at the code of it.  I learned about sophisitcated was of structuring `Dockerfile`s, where and when to use Bash scripting when you need it (you can't just do everything with Python, as much as you might want to), etc.
