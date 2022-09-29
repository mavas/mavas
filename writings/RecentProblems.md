# Recent technical problems being worked on

- [Boost MPI example, using only Docker](boost_mpi_example.md)
- [Docker compose](DockerCompose.md)
- [EOTK and Datalab container review](eotk_datalab.md)
- [A random Arduino kit to play with](arduino.md)
- [Deployment on www.PythonAnywhere.com](python_anywhere.md)
- [Urgent shutdown of cloud resources](cloud_shutdown.md)
- [Failed laptop encrypted hard drive](failed_hard_drive.md)

## The OpenCourt Project

OpenCourt is a web site that lets users create/operate/conduct virtual criminal/civil court cases.  It's essentially a case management system.  The project also features a *simulation* component, which uses a separate asynchronous service which periodically sends text messages and emails to users - at the appropriate time - so that it lets the users really **feel**, in real time, the events portrayed in the court cases.  The intent is that it lets people create court cases and be lawyers or judges within those court cases without actually going to or dealing with a real/legal court.

- **High quality search functionality**.  This is very important, as the vast majority of the content is just text, and is always related to events in time, and you would want to search it.  [Whoosh](https://github.com/mchaput/whoosh) will be used.

- **Opinion measurement**.  Crucial to the system, is that all **opinions** about a court case can be measured.  Practically every court case in America has and makes *decisions* that are very very **fuzzy**; that is, the judge talks back and forth with the lawyers, and then when that's all over, they make some marks on exactly a single sheet of paper which **records the results** of all that discussion, and that's it; all you have is a single sheet of paper.  OpenCourt measures and deals which *all* of the in-between stuff.

- **Strong internationalization language support**.  Lots of members of the public from different backgrounds, and that speak different languages, will need to use the system.  Django's support will be 100% used.

- Emphasis on **testing**.  There is lots of thoughts and opinions and facts and dependencies between them Lots of common folk people will need to use the system.  Use only Django's testing system.
