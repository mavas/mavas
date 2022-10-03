# EOTK and Datalab containers

- github.com/alecmuffett/eotk/opt.d/build-ubuntu-20.04.sh

## Reading the datalab source code

I don't remember being required to dive into the code of Google Cloud's [Datalab](https://github.com/googledatalab/datalab), but I did anyway and was impressed by how it was built.  It really shows what someone could do if they have a **wide** variety of experience, because this project definitely took into account, and integrated, a number of various technologies, to produce a new and clean product: bash scripting, Docker, NodeJS, web development, and security.

The project is somewhat obsolete now, with the new [JupyterLab](https://jupyter.org/) project being the next generation of Datalab, but it was still good to look at the code of it.  I learned about sophisitcated was of structuring `Dockerfile`s, where and when to use Bash scripting when you need it (you can't just do everything with Python, as much as you might want to), etc.

## EOTK scholarly research listing of components

- [this](https://github.com/alecmuffett/eotk/blob/21b506623a18a1b7baa1dcc97adb4299db9370c8/opt.d/lib.sh#L63) line of this Bash script seems to indicate that this whole `eotk`'s latest version of Tor source code considered is `0.4.5.8` (and the latest is `0.4.7.10`).  The shell scripts seem to build from source while the Docker image installs from Ubuntu's package management system; for this project, building from source will likely be prefered.
- And, when building from source, the shell scripts seem to suggest running the `./configure` scripts with only the ``--prefix`` option, like

```
./configure --prefix="$install_dir" "$@" || exit 1
```

- There are 2 methods considered to build the software: with Docker, and via shell scripts.  I'm pretty sure that they both effectively do different things, and so that may be an upstream problem, but I'm not sure, but this is worth noting (in other words, it's supposed to be intended that 2 different build methods produce the same thing, but it looks like that in this case that's not true).
- `onionbalance` Python package and `eotk` command line tool.  [this](https://github.com/alecmuffett/eotk/blob/230c9f83e905024f3abbd2266d85595172df1a58/docs.d/HOW-TO-INSTALL.md#onionbalance-and-load-balancing) section recommends **not** using `onionbalance` and thankfully we won't be going to.
- The `eotk` command line tool looks significant.
- [this](https://github.com/dustyfresh/OnionIRC) page suggests directly running `openssl` command to generate your Onion certificates; this makes me wonder what the `eotk` command employs.
- `https://github.com/FiloSottile/mkcert` is a recommended tool.
- `OpenRESTy` for nginx.  Not at all interesting.
- `ngx_http_substitutions_filter_module` ngnix filter.  Not at all interesting.
- Lots of bash scripts (.sh), and some perl scripts

## EOTK things learned

- I only recently found the sole file responsible for implementing thing `eotk` command; it's the one in the top directory.  It uses the `scp`, `rsync`, `ssh`, commands.  It makes use of some or all of the commands in eotk/opt.d.
- 2 Docker files can be maintained: one that employs the Ubuntu package management system's Tor version for deployment, and another that compiles and employs the `0.4.7.10` (latest) version of Tor.  The main difference is the proper exercise of the Docker's feature of ***multi-stage builds***.
- It saves a lot of thinking and deployment work regarding proper deployment of something like Tor, especially the [my own project!](https://github.com/alecmuffett/eotk/blob/230c9f83e905024f3abbd2266d85595172df1a58/docs.d/HOW-TO-INSTALL.md#i-want-to-create-my-own-project) section of the [install](https://github.com/alecmuffett/eotk/blob/230c9f83e905024f3abbd2266d85595172df1a58/docs.d/HOW-TO-INSTALL.md#L472) documentation.
- This entire project is all much more work than it takes to get the Docker version of I2P working.

The project is mostly about security and there's not much new or novel source code.  I'm mostly grateful that it took care of a lot of security-related thinking and concerns and even training, like regarding SSL certificates and HTTPS.

It did imploy some things that I don't care too much about, like nginx, that regex module that it uses, or OpenResty.
