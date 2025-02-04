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
  - {doc}`version-control/motivation`
  - {doc}`version-control/browsing`
  - {doc}`version-control/branching-and-committing`

- 11:30-12:15 - Lunch break

- 12:15-13:30 - {doc}`version-control` (2/2)
  - {doc}`version-control/merging`
  - {doc}`version-control/conflict-resolution`
  - {doc}`version-control/practical-advice`
  - {doc}`version-control/sharing`

- 13:45-15:00 - {doc}`documentation`


### Tuesday

- 09:00-10:00 - {doc}`collaboration` (1/2)
  - {doc}`collaboration/concepts`
  - {doc}`collaboration/same-repository`

- 10:15-11:30 - {doc}`collaboration` (2/2)
  - {doc}`collaboration/code-review`
  - {doc}`collaboration/forking-workflow`

- 11:30-12:15 - Lunch break

- 12:15-12:45 - {doc}`dependencies`

- 12:45-13:30 - Working with Notebooks
  - {doc}`notebooks/version-control`
  - {doc}`notebooks/tooling`
  - {doc}`notebooks/sharing`

- 13:30-14:15 - Other useful tools for Python development
  - {doc}`good-practices`
  - {doc}`profiling`

- 14:15-15:00 - Debriefing and Q&A
  - Participants work on their projects
  - Together we study actual codes that participants wrote or work on
  - Constructively we discuss possible improvements
  - Give individual feedback on code projects


### Wednesday

- 09:00-10:00 - {doc}`testing`

- 10:15-11:30 - Modular code development
  - {doc}`refactoring-concepts`
  - {doc}`snakemake`

- 11:30-12:15 - Lunch break

- 12:15-14:00 - How to release and publish your code
  - {doc}`software-licensing`
  - {doc}`publishing`
  - {doc}`packaging`

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
notebooks/version-control
notebooks/tooling
notebooks/sharing
good-practices
profiling
testing
refactoring-concepts
snakemake
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
