# Reproducible research software development using Python (ML example)


## Big-picture goal

This is a **hands-on course on research software engineering**. In this
workshop we assume that most workshop participants use Python in their work or
are leading a group which uses Python.  Therefore, some of the examples will use
Python as the example language.

We will work with an example project ({doc}`example`)
and go through all important steps of a typical
software project.  Once we have seen the building blocks, we will try to **apply
them to own projects**.

:::{prereq} Preparation
1. Get a **GitHub account** following [these instructions](https://coderefinery.github.io/installation/github/).
1. You will need a **text editor**. If you don't have a favorite one, we recommend
   [VS Code](https://coderefinery.github.io/installation/vscode/).
1. **If you prefer to work in the terminal** and not in VS Code, set up these two (skip this if you use VS Code):
   - [Git in the terminal](https://coderefinery.github.io/installation/git-in-terminal/)
   - [SSH or HTTPS connection to GitHub from terminal](https://coderefinery.github.io/installation/ssh/)
1. Follow {doc}`installation` (but we will do this together at the beginning of the workshop).
:::


## Schedule

### Monday

- 09:00-10:00 - Getting started
  - Welcome and introduction
  - {doc}`installation`
  - {doc}`example`

- 10:15-11:30 - {doc}`version-control` (1/2)
  - {doc}`version-control/motivation` (15 min)
  - {doc}`version-control/browsing` (30 min)
  - {doc}`version-control/branching-and-committing` (30 min)

- 11:30-12:15 - Lunch break

- 12:15-13:30 - {doc}`version-control` (2/2)
  - {doc}`version-control/merging` (40 min)
  - {doc}`version-control/conflict-resolution` (30 min)
  - {doc}`version-control/practical-advice` (20 min)
  - {doc}`version-control/sharing` (30 min)

- 13:45-15:00 - {doc}`documentation`


### Tuesday

- 09:00-10:00 - {doc}`collaboration` (1/3)
  - {doc}`collaboration/concepts` (15 min)
  - {doc}`collaboration/same-repository` (45 min)

- 10:15-11:30 - {doc}`collaboration` (2/3)
  - {doc}`collaboration/code-review` (35 min)
  - {doc}`collaboration/forking-workflow` (35 min)

- 11:30-12:15 - Lunch break

- 12:15-13:00 - {doc}`collaboration` (3/3)
  - {doc}`collaboration/demo-discussion` (45 min)

- 13:15-14:00 - {doc}`dependencies`

- 14:15-15:00 - Debriefing and Q&A
  - Participants work on their projects
  - Together we study actual codes that participants wrote or work on
  - Constructively we discuss possible improvements
  - Give individual feedback on code projects


### Wednesday

- 09:00-10:00 - {doc}`testing`

- 10:15-11:30 - Code quality and good practices
  - Tools
  - Concepts in refactoring and modular code design
  - Concepts in refactoring and modular code design
  - From a notebook to a script to a workflow
  - Good practices
  - {doc}`profiling`

- 11:30-12:15 - Lunch break

- 12:15-14:00 - How to release and publish your code
  - {doc}`software-licensing` (30 min)
  - {doc}`publishing` (15 min)
  - {doc}`packaging` (45 min)

- 14:15-15:00 - Debriefing and Q&A
  - Participants work on their projects
  - Together we study actual codes that participants wrote or work on
  - Constructively we discuss possible improvements
  - Give individual feedback on code projects


### Thursday

- 09:00-15:00
  - Moving from laptop to high-performance computing (demo/type-along)
  - Introduction to the exam


:::{toctree}
:maxdepth: 1
:caption: Software environment
:hidden:

installation.md
:::


:::{toctree}
:maxdepth: 1
:caption: Episodes
:hidden:

example
version-control
documentation
collaboration
dependencies
testing
profiling
software-licensing
publishing
packaging
:::


:::{toctree}
:maxdepth: 1
:caption: Reference
:hidden:

PDF version <https://coderefinery.github.io/reproducible-python-ml/lesson.pdf>
credit
All lessons <https://coderefinery.org/lessons/>
CodeRefinery <https://coderefinery.org/>
Reusing <https://coderefinery.org/lessons/reusing/>
:::
