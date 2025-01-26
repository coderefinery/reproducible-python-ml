# Motivation

:::{objectives}
- Browse **commits** and **branches** of a Git repository.
- Remember that commits are like **snapshots** of the repository at a certain
  point in time.
- Know the difference between **Git** (something that tracks changes) and
  **GitHub/GitLab** (a web platform to host Git repositories).
:::


## Why do we need to keep track of versions?

Version control is an answer to the following questions (do you recognize some
of them?):

- "It broke ... hopefully I have a working version somewhere?"

- "Can you please send me the latest version?"

- "Where is the latest version?"

- "Which version are you using?"

- "Which version have the authors used in the paper I am trying to reproduce?"

- "Found a bug! Since when was it there?"

- "I am sure it used to work. When did it change?"

- "My laptop is gone. Is my thesis now gone?"


## Demonstration

- Example repository: <https://github.com/workshop-material/classification-task>
- Commits are like **snapshots** and if we break something we can go back to a
  previous snapshot.
- Commits carry **metadata** about changes: author, date, commit message, and
  a checksum.
- **Branches** are like parallel universes where you can experiment with
  changes without affecting the default branch:
  <https://github.com/workshop-material/classification-task/network>
  ("Insights" -> "Network")
- With version control we can **annotate code**
  ([example](https://github.com/workshop-material/classification-tas/blame/main/generate_predictions.py)).
- **Collaboration**: We can fork (make a copy on GitHub), clone (make a copy
  to our computer), review, compare, share, and discuss.
- **Code review**: Others can suggest changes using pull requests or merge
  requests. These can be reviewed and discussed before they are merged.
  Conceptually, they are similar to "suggesting changes" in Google Docs.


## Features: roll-back, branching, merging, collaboration

- **Roll-back**: you can always go back to a previous version and compare

- **Branching and merging**:
  - Work on different ideas at the same time
  - You can experiment with an idea and discard it if it turns out to be a bad idea
  - Different people can work on the same code/project without interfering

:::{figure} img/gophers.png
:alt: Branching explained with a gopher
:width: 100%

Image created using <https://gopherize.me/>
([inspiration](https://twitter.com/jay_gee/status/703360688618536960)).
:::

- **Collaboration**: review, compare, share, discuss

- [Example network graph](https://github.com/workshop-material/classification-task/network)


## Talking about code

Which of these two is more practical?
1. "Clone the code, go to the file 'generate_predictions.py', and search for 'majority_index'.
   Oh! But make sure you use the version from January 2025."
1. Or I can send you a permalink: <https://github.com/workshop-material/classification-task/blob/79ce3be8/generate_predictions.py#L25-L28>


## What we typically like to snapshot

- Software (this is how it started but Git/GitHub can track a lot more)
- Scripts
- Documents (plain text files much better suitable than Word documents)
- Manuscripts (Git is great for collaborating/sharing LaTeX or [Quarto](https://quarto.org/) manuscripts)
- Configuration files
- Website sources
- Data

::::{discussion}
  In this example somebody tried to keep track of versions without a version
  control system tool like Git.  Discuss the following directory listing. What
  possible problems do you anticipate with this kind of "version control":
  ```text
  myproject-2019.zip
  myproject-2020-february.zip
  myproject-2021-august.zip
  myproject-2023-09-19-working.zip
  myproject-2023-09-21.zip
  myproject-2023-09-21-test.zip
  myproject-2023-09-21-myversion.zip
  myproject-2023-09-21-newfeature.zip
  ...
  (100 more files like these)
  ```

  :::{solution}
  - Giving a version to a collaborator and merging changes later with own
    changes sounds like lots of work.
  - What if you discover a bug and want to know since when the bug existed?
  :::
::::
