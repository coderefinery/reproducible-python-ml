# Reproducible environments and dependencies

:::{objectives}
- There are not many codes that have no dependencies.
  How should we **deal with dependencies**?
- We will focus on installing and managing dependencies in Python when using packages from PyPI and Conda.
- We will not discuss how to distribute your code as a package.
:::

[This episode borrows from <https://coderefinery.github.io/reproducible-python/reusable/>
and <https://aaltoscicomp.github.io/python-for-scicomp/dependencies/>]

Essential XKCD comics:
- [xkcd - dependency](https://xkcd.com/2347/)
- [xkcd - superfund](https://xkcd.com/1987/)


## How to avoid: "It works on my machine &#129335;"

Use a **standard way** to list dependencies in your project:
- Python: `requirements.txt` or `environment.yml`
- R: `DESCRIPTION` or `renv.lock`
- Rust: `Cargo.lock`
- Julia: `Project.toml`
- C/C++/Fortran: `CMakeLists.txt` or `Makefile` or `spack.yaml` or the module
  system on clusters or containers
- Other languages: ...


## Two ecosystems: PyPI (The Python Package Index) and Conda

:::{admonition} PyPI
- **Installation tool:** `pip` or `uv` or similar
- Traditionally used for Python-only packages or
  for Python interfaces to external libraries. There are also packages
  that have bundled external libraries (such as numpy).
- **Pros:**
    - Easy to use
    - Package creation is easy
- **Cons:**
    - Installing packages that need external libraries can be complicated
:::

:::{admonition} Conda
- **Installation tool:** `conda` or `mamba` or similar
- Aims to be a more general package distribution tool
  and it tries to provide not only the Python packages, but also libraries
  and tools needed by the Python packages.
- **Pros:**
    - Quite easy to use
    - Easier to manage packages that need external libraries
    - Not only for Python
- **Cons:**
    - Package creation is harder
:::


## Conda ecosystem explained

- [Anaconda](https://www.anaconda.com) is a distribution of conda packages
  made by Anaconda Inc. When using Anaconda remember to check that your
  situation abides with their licensing terms (see below).

- Anaconda has recently changed its **licensing terms**, which affects its
  use in a professional setting. This caused uproar among academia
  and Anaconda modified their position in
  [this article](https://www.anaconda.com/blog/update-on-anacondas-terms-of-service-for-academia-and-research).

   Main points of the article are:
   - conda (installation tool) and community channels (e.g. conda-forge)
     are free to use.
   - Anaconda repository and **Anaconda's channels in the community repository**
     are free for universities and companies with fewer than 200 employees.
     Non-university research institutions and national laboratories need
     licenses.
   - Miniconda is free, when it does not download Anaconda's packages.
   - Miniforge is not related to Anaconda, so it is free.

   For ease of use on sharing environment files, we recommend using
   Miniforge to create the environments and using conda-forge as the main
   channel that provides software.

- Major repositories/channels:
  - [Anaconda Repository](https://repo.anaconda.com)
    houses Anaconda's own proprietary software channels.
  - Anaconda's proprietary channels: `main`, `r`, `msys2` and `anaconda`.
    These are sometimes called `defaults`.
  - [conda-forge](https://conda-forge.org) is the largest open source
    community channel. It has over 28k packages that include open-source
    versions of packages in Anaconda's channels.


## Tools and distributions for dependency management in Python

- [Poetry](https://python-poetry.org): Dependency management and packaging.
- [Pipenv](https://pipenv.pypa.io): Dependency management, alternative to Poetry.
- [pyenv](https://github.com/pyenv/pyenv): If you need different Python versions for different projects.
- [virtualenv](https://docs.python.org/3/library/venv.html): Tool to create isolated Python environments for PyPI packages.
- [micropipenv](https://github.com/thoth-station/micropipenv): Lightweight tool to "rule them all".
- [Conda](https://docs.conda.io): Package manager for Python and other languages maintained by Anaconda Inc.
- [Miniconda](https://docs.anaconda.com/miniconda/): A "miniature" version of conda, maintained by Anaconda Inc. By default uses
  Anaconda's channels. Check licensing terms when using these packages.
- [Mamba](https://mamba.readthedocs.io): A drop in replacement for conda.
  It used be much faster than conda due to better
  dependency solver but nowadays conda
  [also uses the same solver](https://conda.org/blog/2023-11-06-conda-23-10-0-release/).
  It still has some UI improvements.
- [Micromamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html): Tiny version of the Mamba package manager.
- [Miniforge](https://github.com/conda-forge/miniforge): Open-source Miniconda alternative with
  conda-forge as the default channel and optionally mamba as the default installer.
- [Pixi](https://pixi.sh): Modern, super fast tool which can manage conda environments.
- [uv](https://docs.astral.sh/uv/): Modern, super fast replacement for pip,
  poetry, pyenv, and virtualenv. You can also switch between Python versions.


## Best practice: Install dependencies into isolated environments

- For each project, create a **separate environment**.
- Don't install dependencies globally for all projects. Sooner or later, different projects will have conflicting dependencies.
- Install them **from a file** which documents them at the same time
  Install dependencies by first recording them in `requirements.txt` or
  `environment.yml` and install using these files, then you have a trace
  (we will practice this later below).

:::{keypoints}
If somebody asks you what dependencies you have in your project, you should be
able to answer this question **with a file**.

In Python, the two most common ways to do this are:
- **requirements.txt** (for pip and virtual environments)
- **environment.yml** (for conda and similar)

You can export ("freeze") the dependencies from your current environment into these files:
```bash
# inside a conda environment
$ conda env export --from-history > environment.yml

# inside a virtual environment
$ pip freeze > requirements.txt
```
:::


## How to communicate the dependencies as part of a report/thesis/publication

Each notebook or script or project which depends on libraries should come with
either a `requirements.txt` or a `environment.yml`, unless you are creating
and distributing this project as Python package.

- Attach a `requirements.txt` or a `environment.yml` to your thesis.
- Even better: Put `requirements.txt` or a `environment.yml` in your Git repository along your code.
- Even better: Also [binderize](https://mybinder.org/) your analysis pipeline.


## Containers

- A container is like an **operating system inside a file**.
- "Building a container": Container definition file (recipe) -> Container image
- This can be used with [Apptainer](https://apptainer.org/)/
  [SingularityCE](https://sylabs.io/singularity/).

Containers offer the following advantages:
- **Reproducibility**: The same software environment can be recreated on
  different computers. They force you to know and **document all your dependencies**.
- **Portability**: The same software environment can be run on different computers.
- **Isolation**: The software environment is isolated from the host system.
- "**Time travel**":
  - You can run old/unmaintained software on new systems.
  - Code that needs new dependencies which are not available on old systems can
    still be run on old systems.


## How to install dependencies into environments

Now we understand a bit better why and how we installed dependencies
for this course in the {doc}`installation`.

We have used **Miniforge** and the long command we have used was:
```console
$ mamba env create -n course -f https://raw.githubusercontent.com/coderefinery/python-progression/main/software/environment.yml
```

This command did two things:
- Create a new environment with name "course" (specified by `-n`).
- Installed all dependencies listed in the `environment.yml` file (specified by
  `-f`), which we fetched directly from the web.
  [Here](https://github.com/coderefinery/python-progression/blob/main/software/environment.yml)
  you can browse it.

For your own projects:
1. Start by writing an `environment.yml` of `requirements.txt` file. They look like this:
:::::{tabs}
  ::::{tab} environment.yml
    :::{literalinclude} ../software/environment.yml
    :language: yaml
    :::
  ::::

  ::::{tab} requirements.txt
    :::{literalinclude} ../software/requirements.txt
    :::
  ::::
:::::

2. Then set up an isolated environment and install the dependencies from the file into it:
:::::{tabs}
  ::::{group-tab} Miniforge
    - Create a new environment with name "myenv" from `environment.yml`:
      ```console
      $ conda env create -n myenv -f environment.yml
      ```
      Or equivalently:
      ```console
      $ mamba env create -n myenv -f environment.yml
      ```
    - Activate the environment:
      ```console
      $ conda activate myenv
      ```
    - Run your code inside the activated virtual environment.
      ```console
      $ python example.py
      ```
  ::::

  ::::{group-tab} Pixi
    - Create `pixi.toml` from `environment.yml`:
      ```console
      $ pixi init --import environment.yml
      ```
    - Run your code inside the environment:
      ```console
      $ pixi run python example.py
      ```
  ::::

  ::::{group-tab} Virtual environment
    - Create a virtual environment by running (the second argument is the name
      of the environment and you can change it):
      ```console
      $ python -m venv venv
      ```
    - Activate the virtual environment (how precisely depends on your operating
      system and shell).
    - Install the dependencies:
      ```console
      $ python -m pip install -r requirements.txt
      ```
    - Run your code inside the activated virtual environment.
      ```console
      $ python example.py
      ```
  ::::

  ::::{group-tab} uv
    - Create a virtual environment by running (the second argument is the name
      of the environment and you can change it):
      ```console
      $ uv venv venv
      ```
    - Activate the virtual environment (how precisely depends on your operating
      system and shell).
    - Install the dependencies:
      ```console
      $ uv pip sync requirements.txt
      ```
    - Run your code inside the virtual environment.
      ```console
      $ uv run python example.py
      ```
  ::::
:::::


## Updating environments

What if you forgot a dependency? Or during the development of your project
you realize that you need a new dependency? Or you don't need some dependency anymore?

1. Modify the `environment.yml` or `requirements.txt` file.
2. Either remove your environment and create a new one, or update the existing one:

:::::{tabs}
  ::::{group-tab} Miniforge
    - Update the environment by running:
      ```console
      $ conda env update --file environment.yml
      ```
    - Or equivalently:
      ```console
      $ mamba env update --file environment.yml
      ```
  ::::

  ::::{group-tab} Pixi
    - Remove `pixi.toml`.
    - Then update it from the updated `environment.yml` by running:
      ```console
      $ pixi init --import environment.yml
      ```
  ::::

  ::::{group-tab} Virtual environment
    - Activate the virtual environment.
    - Update the environment by running:
      ```console
      $ pip install -r requirements.txt
      ```
  ::::

  ::::{group-tab} uv
    - Activate the virtual environment.
    - Update the environment by running:
      ```console
      $ uv pip sync requirements.txt
      ```
  ::::
:::::


## Pinning package versions

Let us look at the
[environment.yml](https://github.com/coderefinery/python-progression/blob/main/software/environment.yml)
which we used to set up the environment for this progression course.
Dependencies are listed without version numbers. Should we **pin the
versions**?

- Both `pip` and `conda` ecosystems and all the tools that we have
  mentioned support pinning versions.

- It is possible to define a range of versions instead of precise versions.

- While your project is still in progress, I often use latest versions and do not pin them.

- When publishing the script or notebook, it is a good idea to pin the versions
  to ensure that the code can be run in the future.

- Remember that at some point in time you will face a situation where
  newer versions of the dependencies are no longer compatible with your
  software. At this point you'll have to update your software to use the newer
  versions or to lock it into a place in time.


## Managing dependencies on a supercomputer

- Additional challenges:
  - Storage quotas: **Do not install dependencies in your home directory**. A conda environment can easily contain 100k files.
  - Network file systems struggle with many small files. Conda environments often contain many small files.
- Possible solutions:
  - Try [Pixi](https://pixi.sh/) (modern take on managing Conda environments) and
    [uv](https://docs.astral.sh/uv/) (modern take on managing virtual
    environments). Blog post: [Using Pixi and uv on a supercomputer](https://research-software.uit.no/blog/2025-pixi-and-uv/)
  - Install your environment on the fly into a scratch directory on local disk (**not** the network file system).
  - Install your environment on the fly into a RAM disk/drive.
  - Containerize your environment into a container image.

---

:::{keypoints}
- Being able to communicate your dependencies is not only nice for others, but
  also for your future self or the next PhD student or post-doc.
- If you ask somebody to help you with your code, they will ask you for the
  dependencies.
:::
