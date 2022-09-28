# Recent technical problems being worked on

- [Boost MPI example, using only Docker](boost_mpi_example.md)
- [Docker compose](DockerCompose.md)
- [EOTK and Datalab container review](eotk_datalab.md)
- [A random Arduino kit to play with](arduino.md)
- [Deployment on www.PythonAnywhere.com](python_anywhere.md)
- [Urgent shutdown of cloud resources](cloud_shutdown.md)
- [Failed laptop encrypted hard drive](failed_hard_drive.md)

### Docker files understanding

I've had to manually understand and craft and modify many Dockerfiles seen in the wild lately for this project, and so this section lists them all.  Effort was made to use the same Ubuntu version everywhere.

- github.com/alecmuffett/eotk/opt.d/build-ubuntu-20.04.sh

## Failed laptop encrypted hard drive

_Linux Unified Key Setup, reading its source code, learning its commands, and running 'dd'_

I came home to find that my primary laptop's hard drive failed, and I had to just deal with it.  I had to learn and deal with the LUKS Linux encryption file system thing, not only having to discover/learn/run new commands (like `cryptsetup`, and `luksOpen`), but dealing with the source code itself **of** those command line tools.  All of the data was valuable, so I had to be careful, and so I had to know exactly what was going on, so dealing with these commands, and  their source code, was important to proceed with; thankfully the code was rather short.  I had to run the **dd if=/dev/sda of=/dev/sdb** command in attempts to at least perfectly mirror/backup the data, so that you can simply install Ubuntu back on it and the hard drive will be good as new, but I ran in to some errors with that command, and so now I'm stuck, and the laptop is just sitting here.  In the meantime it was fastest though to just use my older laptop for job hunting, and then get a job, and then get back to the issue.  Anyway, I usually use Ubuntu, and sometimes its using some transperant encryption thing underneath as the file system, and the point is is that it really is a transperant thing, meaning you're not supposed to really need to think about it.  But with this issue, it suddenly became **the** issue and one then has to dig under the hood and discover and learn about and deal with yet another new layer of software *stuff*.

## The OpenCourt Project

OpenCourt is a web site that lets users create/operate/conduct virtual criminal/civil court cases.  It's essentially a case management system.  The project also features a *simulation* component, which uses a separate asynchronous service which periodically sends text messages and emails to users - at the appropriate time - so that it lets the users really **feel**, in real time, the events portrayed in the court cases.  The intent is that it lets people create court cases and be lawyers or judges within those court cases without actually going to or dealing with a real/legal court.

- **High quality search functionality**.  This is very important, as the vast majority of the content is just text, and is always related to events in time, and you would want to search it.  [Whoosh](https://github.com/mchaput/whoosh) will be used.

- **Opinion measurement**.  Crucial to the system, is that all **opinions** about a court case can be measured.  Practically every court case in America has and makes *decisions* that are very very **fuzzy**; that is, the judge talks back and forth with the lawyers, and then when that's all over, they make some marks on exactly a single sheet of paper which **records the results** of all that discussion, and that's it; all you have is a single sheet of paper.  OpenCourt measures and deals which *all* of the in-between stuff.

- **Strong internationalization language support**.  Lots of members of the public from different backgrounds, and that speak different languages, will need to use the system.  Django's support will be 100% used.

- Emphasis on **testing**.  There is lots of thoughts and opinions and facts and dependencies between them Lots of common folk people will need to use the system.  Use only Django's testing system.

## Reading the datalab source code

I don't remember being required to dive into the code of Google Cloud's [Datalab](https://github.com/googledatalab/datalab), but I did anyway and was impressed by how it was built.  It really shows what someone could do if they have a **wide** variety of experience, because this project definitely took into account, and integrated, a number of various technologies, to produce a new and clean product: bash scripting, Docker, NodeJS, web development, and security.

The project is somewhat obsolete now, with the new [JupyterLab](https://jupyter.org/) project being the next generation of Datalab, but it was still good to look at the code of it.  I learned about sophisitcated was of structuring `Dockerfile`s, where and when to use Bash scripting when you need it (you can't just do everything with Python, as much as you might want to), etc.
