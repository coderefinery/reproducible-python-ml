# Forking, cloning, and browsing

In this episode, we will look at an **existing repository** to understand how
all the pieces work together. Along the way, we will make a copy (by
**forking** and/or **cloning**) of the repository for us, which will be used
for our own changes.

:::{objectives}
- See a real Git repository and understand what is inside of it.
- Understand how version control allows advanced inspection of a
  repository.
- See how Git allows multiple people to work on the same project at the same time.
- **See the big picture** instead of remembering a bunch of commands.
:::


## GitHub, VS Code, or command line

We offer **three different paths** for this exercise:
- **GitHub** (this is the one we will demonstrate)
- **VS Code** (if you prefer to follow along using an editor)
- **Command line** (for people comfortable with the command line)


## Creating a copy of the repository by "forking" or "cloning"

A **repository** is a collection of files in one directory tracked by Git.  A
GitHub repository is GitHub's copy, which adds things like access control,
issue tracking, and discussions.  Each GitHub repository is owned by a user or
organization, who controls access.

First, we need to make **our own copy** of the exercise repository. This will
become important later, when we make our own changes.

:::{figure} img/illustrations/fork.png
:alt: Illustration of forking a repository on GitHub
:width: 50%

Illustration of forking a repository on GitHub.
:::

:::{figure} img/illustrations/clone.png
:alt: Illustration of cloning a repository to your computer
:width: 50%

Illustration of cloning a repository to your computer.
:::

:::{figure} img/illustrations/clone-of-fork.png
:alt: Illustration of cloning a forked repository to your computer
:width: 60%

It is also possible to do this: to clone a forked repository to your computer.
:::

At all times you should be aware of if you are looking at **your repository**
or the **upstream repository** (original repository):
- Your repository: https://github.com/**USER**/planets
- Upstream repository: https://github.com/**workshop-material**/planets

:::{admonition} How to create a fork
1. Go to the repository view on GitHub: <https://github.com/workshop-material/planets>
1. First, on GitHub, click the button that says "Fork". It is towards
   the top-right of the screen.
1. You should shortly be redirected to your copy of the repository
   **USER/planets**.
:::

:::{instructor-note}
Before starting the exercise session show
how to fork the repository to own account
(above).
:::



## Exercise: Copy and browse an existing project

Work on this by yourself or in pairs.












::::::{prereq} Exercise preparation
:::::{tabs}
::::{group-tab} GitHub
In this case you will work on a fork.

You only need to open your own view, as described above.  The browser
URL should look like https://github.com/**USER**/planets, where
USER is your GitHub username.
::::

::::{group-tab} VS Code
You need to have forked the repository as described above.

We need to start by making a clone of this repository so that you can work
locally.

1. Start VS Code.
1. If you don't have the default view (you already have a project
open), go to File → New Window.
1. Under "Start" on the screen, select "Clone Git Repository...". Alternatively
   navigate to the "Source Control" tab on the left sidebar and click on the "Clone Repository" button.
1. Paste in this URL: `https://github.com/USER/planets`, where
   `USER` is your username.  You can copy this from the browser.
1. Browse and select the folder in which you want to clone the
   repository.
1. Say yes, you want to open this repository.
1. Select "Yes, I trust the authors" (the other option works too).
::::

::::{group-tab} Command line
**This path is advanced and we do not include all command line
information: you need to be somewhat
comfortable with the command line already.**

You need to have forked the repository as described above.

We need to start by making a clone of this repository so that you can work
locally.

1. Start the terminal in which you use Git (terminal application, or
   Git Bash).
1. Change to the directory where you would want the repository to be
   (`cd ~/code` for example, if the `~/code` directory is where you
   store your files).
1. Run the following command: `git clone
   https://github.com/USER/planets`, where `USER` is your
   username.  You might need to use a SSH clone command instead of
   HTTPS, depending on your setup.
1. Change to that directory: `cd planets`
::::
:::::
::::::


:::{exercise} Exercise: Browsing an existing project (20 min)

Browse the [example project](https://github.com/workshop-material/planets) and
explore commits and branches, either on a fork or on a clone.  Take notes and
prepare questions.  The hints are for the GitHub path in the browser.

1. Browse the **commit history**: Are commit messages understandable?
   (Hint: "Commit history", the timeline symbol, above the file list)
1. Compare the commit history with the **network graph** ("Insights" -> "Network"). Can you find the branches?
1. Try to find the **history of commits for a single file**, e.g. `simulate.py`.
   (Hint: "History" button in the file view)
1. **Which files include the word "position"**?
   (Hint: the GitHub search on top of the repository view)
1. In the `simulate.py` file,
   find out who modified the "time step"
   last and **in which commit**.
   (Hint: "Blame" view in the file view)
1. Can you use this code yourself? **Are you allowed to share
   modifications**?
   (Hint: look for a license file)
:::

The solution below goes over most of the answers, and you are
encouraged to use it when the hints aren't enough - this is by
design.


## Solution and walk-through

### (1) Basic browsing

The most basic thing to look at is the history of commits.

* This is visible from a button in the repository view.  We see every
  change, when, and who has committed.
* Every change has a unique identifier, such as `244c993`.  This can
  be used to identify both this change, and the whole project's
  version as of that change.
* Clicking on a change in the view shows more.

:::::{tabs}

::::{group-tab} GitHub
Click on the timeline symbol in the repository view:
  :::{figure} img/browsing/history.png
  :alt: Screenshot on GitHub of where to find the commit history
  :width: 100%
  :class: with-border
  :::
::::

::::{group-tab} VS Code
This can be done from "Timeline", in the bottom of explorer, but only
for a single file.
::::

::::{group-tab} Command line
Run:
```console
$ git log
```

Try also:
```console
$ git log --oneline
```
::::

:::::


### (2) Compare commit history with network graph

The commit history we saw above looks linear: one commit after
another.  But if we look at the network view, we see some branching and merging points.
We'll see how to do these later.  This is another one of the
basic Git views.

:::::{tabs}
::::{group-tab} GitHub
In a new browser tab, open the "Insights" tab, and click on "Network".
You can hover over the commit dots to see the person who committed and
how they correspond with the commits in the other view:
  :::{figure} img/browsing/network.png
  :alt: Screenshot on GitHub of the network graph
  :width: 100%
  :class: with-border
  :::
::::

::::{group-tab} VS Code
We don't know how to do this without an extension. Try starting a terminal and using the
"Command line" option.
::::

::::{group-tab} Command line
This is a useful command to browse the network of commits locally:
```console
$ git log --graph --oneline --decorate --all
```

To avoid having to type this long command every time, you can define an alias (shortcut):
```console
$ git config --global alias.graph "log --graph --oneline --decorate --all"
```

From then on, you can use `git graph` to see the network graph.
::::

:::::


### (3) How can you browse the history of a single file?

We see the history for the whole repository, but we can also see it
for a single file.

:::::{tabs}

::::{group-tab} GitHub
Navigate to the file view: Main page → simulate.py.
Click the "History" button near the top right.
::::

::::{group-tab} VS Code
Open simulate.py file in the editor.  Under the file browser,
we see a "Timeline" view there.
::::

::::{group-tab} Command line
The `git log` command can take a filename and provide the log of only
a single file:

```
$ git log simulate.py
```
::::

:::::


### (4) Which files include the word "position"?

Version control makes it very easy to find all occurrences of a
word or pattern. This is useful for things like finding where functions or
variables are defined or used.

:::::{tabs}
::::{group-tab} GitHub
We go to the main file view.  We click the Search magnifying
class at the very top, type "position", and click enter. We see every
instance, including the context.

:::{admonition} Searching in a forked repository will not work instantaneously!

It usually takes a few minutes before one can search for keywords in a forked repository
since it first needs to build the search index the very first time we search.
Start it, continue with other steps, then come back to this.
:::
::::

::::{group-tab} VS Code
If you use the "Search" magnifying class on the left sidebar, and
search for "position" it shows the occurrences in every file. You can
click to see the usage in context.
::::

::::{group-tab} Command line
`grep` is the command line tool that searches for lines matching a term
```console
$ git grep position          # only the lines
$ git grep -C 3 position     # three lines of context
$ git grep -i position       # case insensitive
```
::::

:::::


### (5) Who modified a particular line last and when?

This is called the "annotate" or "blame" view. The name "blame"
is very unfortunate, but it is the standard term for historical reasons
for this functionality and it is not meant to blame anyone.

:::::{tabs}

::::{group-tab} GitHub
From a file view, change preview to "Blame" towards the top-left.
To get the actual commit, click on the commit message next
to the code line that you are interested in.
::::

::::{group-tab} VS Code
This requires an extension.  We recommend for now you use the command
line version, after opening a terminal.
::::

::::{group-tab} Command line
These two commands are similar but have slightly different output.
```console
$ git annotate simulate.py
$ git blame simulate.py
```
::::

:::::


### (6) Can you use this code yourself? Are you allowed to share modifications?

- Look at the file `LICENSE`.
- On GitHub, click on the file to see a nice summary of what we can do with this:
  :::{figure} img/browsing/license.png
  :alt: Screenshot on GitHub summarizing license terms
  :width: 100%
  :class: with-border
  :::


### Summary

- Git allowed us to understand this simple project much better than we
  could, if it was just a few files on our own computer.
- It was easy to share the project with the course.
- By forking the repository, we created our own copy. This is
  important for the following, where we will make changes to
  our copy.
