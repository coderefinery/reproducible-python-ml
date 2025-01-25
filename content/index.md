# Reproducible research software development using Python (ML example)


## Big-picture goal

This is a **hands-on course on research software engineering**. In this
workshop we assume that most workshop participants use Python in their work or
a leading a group which uses Python.  Therefore, some of the examples will use
Python as the example language.

We will work with an example project and go through all important steps of a typical
software project.  Once we have seen the building blocks, we will try to **apply
them to own projects**.


## Prerequisites

:::{prereq} Preparation
1. Get a **GitHub account** following [these instructions](https://coderefinery.github.io/installation/github/).
1. You will need a **text editor**. If you don't have a favorite one, we recommend
   [VS Code](https://coderefinery.github.io/installation/vscode/).
1. **If you prefer to work in the terminal** and not in VS Code, set up these two (skip this if you use VS Code):
   - [Git in the terminal](https://coderefinery.github.io/installation/git-in-terminal/)
   - [SSH or HTTPS connection to GitHub from terminal](https://coderefinery.github.io/installation/ssh/)
1. **One of these two software environments** (if you are not sure which one to
   choose or have no preference, choose Conda):
   - {ref}`conda`
   - {ref}`venv` (Snakemake is not available in this environment)
1. **Optional** and only on Linux: [Apptainer](https://apptainer.org/) following
   [these instructions](https://apptainer.org/docs/admin/1.3/installation.html#install-from-pre-built-packages).
:::


## Schedule

### Day 1

- 13:00-13:30 - **Welcome and introduction**
  - Practical information (tools, communication, breaks, etc.)
  - Motivation (reproducibility, robustness, distribution, improvement, trust, etc.)
  - {ref}`example-project`

- 13:30-14:45 - {ref}`version-control` (1/2)
  - {ref}`version-control-motivation` (15 min)
  - {ref}`browsing` (30 min)
  - {ref}`branching-and-committing` (30 min)

- 15:00-16:30 - {ref}`version-control` (2/2)
  - {ref}`merging` (40 min)
  - {ref}`conflict-resolution` (30 min)
  - {ref}`practical-advice` (20 min)
  - {ref}`sharing-repositories` (30 min)

- 16:45-18:00 - {ref}`documentation`


### Day 2

- 09:00-10:30 - {ref}`collaboration` (1/2)
  - {ref}`concepts` (10 min)
  - {ref}`same-repository` (40 min)
  - {ref}`code-review` (40 min)

- 10:45-12:15 - {ref}`collaboration` (2/2)
  - {ref}`forking-workflow` (50 min)
  - {ref}`collaboration-demo-discussion` (40 min)

- 16:45-18:00 - **Debriefing and Q&A**
  - Participants work on their projects
  - Together we study actual codes that participants wrote or work on
  - Constructively we discuss possible improvements
  - Give individual feedback on code projects


### Day 3

- 09:00-10:30 - {ref}`testing`

- 10:45-12:15 - {ref}`reusable`

- 13:00-14:45 - Code quality and good practices
  - {ref}`refactoring-concepts` (15 min)
  - {ref}`refactoring-demo` (90 min)

- 15:00-16:30 - How to release and publish your code
  - {ref}`software-licensing` (30 min)
  - {ref}`publishing` (15 min)
  - {ref}`packaging` (45 min)

- 16:45-18:00 - **Debriefing and Q&A**
  - Participants work on their projects
  - Together we study actual codes that participants wrote or work on
  - Constructively we discuss possible improvements
  - Give individual feedback on code projects


```{toctree}
:maxdepth: 1
:caption: Software environment
:hidden:

installation/conda
installation/virtual-environment
```

```{toctree}
:maxdepth: 1
:caption: Episodes
:hidden:

example
version-control
documentation
collaboration
testing
reusable
refactoring-concepts
refactoring-demo
software-licensing
publishing
packaging
```

```{toctree}
:maxdepth: 1
:caption: Reference
:hidden:

PDF version <https://coderefinery.github.io/reproducible-python/lesson.pdf>
credit
All lessons <https://coderefinery.org/lessons/>
CodeRefinery <https://coderefinery.org/>
Reusing <https://coderefinery.org/lessons/reusing/>
```
