# Notebooks and version control

:::{objectives}
- Demonstrate two tools which make version control of notebooks easier.
:::

[this episode is adapted after <https://coderefinery.github.io/jupyter/version-control/>]

Jupyter Notebooks are stored in [JSON](https://en.wikipedia.org/wiki/JSON) format.
With this format it can be a bit difficult to compare and merge changes which are introduced
through the notebook interface.


## Packages and JupyterLab extensions to simplify version control

Several packages and JupyterLab extensions have been developed
to make it easier to interact with Git and GitHub:

- [nbdime](http://nbdime.readthedocs.io/) (notebook "diff" and "merge") provides
  "content-aware" diffing and merging.
  - Adds a Git button to the notebook interface.
  - `git diff` and `git merge` shell commands can use nbdime's diff
    and merge for notebook files, but leave Git's behavior unchanged
    for non-notebook files.
- [jupyterlab-git](https://github.com/jupyterlab/jupyterlab-git)
  is a JupyterLab extension for version control using Git.
  - Adds a Git tab to the left-side menu bar for version control inside JupyterLab.
- [JupyterLab GitHub](https://www.npmjs.com/package/@jupyterlab/github)
  is a JupyterLab extension for accessing GitHub repositories.
  - Adds a GitHub tab to the left-side menu bar where you can browse
    and open notebooks from your GitHub repositories.

All three extensions can be used from within the JupyterLab interface and our
[Conda
environment](https://coderefinery.github.io/installation/conda/)
provides [jupyterlab-git](https://github.com/jupyterlab/jupyterlab-git) and
[nbdime](http://nbdime.readthedocs.io/).  To install additional extensions,
please consult the [official
documentation](https://jupyterlab.readthedocs.io/en/stable/user/extensions.html)
about installing and managing JupyterLab extensions.

---

## Comparing Jupyter Notebooks on GitHub

For this you really want to enable [Rich Jupyter Notebook
Diffs](https://github.blog/changelog/2023-03-01-feature-preview-rich-jupyter-notebook-diffs/)
on GitHub:
- On GitHub click on your avatar/image (top right).
- Click on "Feature preview".
- Enable "Rich Jupyter Notebook Diffs".

:::{exercise} Demonstration
- We can demonstrate this with a notebook that contains a Matplotlib plot
  (unfortunately the demonstration is less convincing with an Altair plot since the latter
  is generated on the fly and not stored as an image).

- We place the notebook in a GitHub repository and make a small change to it.

- We use https://github.com/**USER**/**REPO**/compare/**VERSION1**..**VERSION2** to
  compare the two versions of the notebook, once with "Rich Jupyter Notebook Diffs" enabled,
  and once without.
:::
