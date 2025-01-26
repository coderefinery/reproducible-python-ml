# Creating a Python package and deploying it to PyPI

:::{objectives}
In this episode we will create a pip-installable Python package and learn how
to deploy it to PyPI. As example, we can use one of the Python scripts from our
example repository.
:::


## Creating a Python package with the help of [Flit](https://flit.pypa.io/)

There are unfortunately many ways to package a Python project:
- `setuptools` is the most common way to package a Python project. It is very
  powerful and flexible, but also can get complex.
- `flit` is a simpler alternative to `setuptools`. It is less versatile, but
  also easier to use.
- `poetry` is a modern packaging tool which is more versatile than `flit` and
  also easier to use than `setuptools`.
- `twine` is another tool to upload packages to PyPI.
- ...

:::{admonition} This will be a demo
- We will try to package the code together on the big screen.
- We will share the result on GitHub so that you can retrace the steps.
- In this demo, we will use Flit to package the code. From [Why use Flit?](https://flit.pypa.io/en/latest/rationale.html):
  > Make the easy things easy and the hard things possible is an old motto from
  > the Perl community. Flit is entirely focused on the easy things part of that,
  > and leaves the hard things up to other tools.
:::


## Step 1: Initialize the package metadata and try a local install

1. Our starting point is that we have a Python script called `example.py`
   which we want to package.

2. Now we follow the [flit quick-start usage](https://flit.pypa.io/en/stable/#usage) and add a docstring to the script and a `__version__`.

3. We then run `flit init` to create a `pyproject.toml` file and answer few questions. I obtained:
   ```{code-block} toml
   ---
   emphasize-lines: 6, 13
   ---
   [build-system]
   requires = ["flit_core >=3.2,<4"]
   build-backend = "flit_core.buildapi"

   [project]
   name = "example"
   authors = [{name = "Firstname Lastname", email = "first.last@example.org"}]
   license = {file = "LICENSE"}
   classifiers = ["License :: OSI Approved :: European Union Public Licence 1.2 (EUPL 1.2)"]
   dynamic = ["version", "description"]

   [project.urls]
   Home = "https://example.org"
   ```
   To have a more concrete example, if we package the `generate_data.py` script
   from the [example
   repository](https://github.com/workshop-material/classification-task), then
   replace the name `example` with `generate_data`.

4. We now add dependencies and also an entry point for the script:
   ```{code-block} toml
   ---
   emphasize-lines: 11-15, 20-21
   ---
   [build-system]
   requires = ["flit_core >=3.2,<4"]
   build-backend = "flit_core.buildapi"

   [project]
   name = "example"
   authors = [{name = "Firstname Lastname", email = "first.last@example.org"}]
   license = {file = "LICENSE"}
   classifiers = ["License :: OSI Approved :: European Union Public Licence 1.2 (EUPL 1.2)"]
   dynamic = ["version", "description"]
   dependencies = [
       "click",
       "numpy",
       "pandas",
   ]

   [project.urls]
   Home = "https://example.org"

   [project.scripts]
   example = "example:main"
   ```

5. Before moving on, try a local install:
   ```console
   $ flit install --symlink
   ```

:::{discussion} What if you have more than just one script?
- Create a directory with the name of the package.
- Put the scripts in the directory.
- Add a `__init__.py` file to the directory which contains the module
  docstring and the version and re-exports the functions from the scripts.
:::


## Step 2: Testing an install from GitHub

If a local install worked, push the `pyproject.toml` to GitHub and try to install the package from GitHub.

In a `requirements.txt` file, you can specify the GitHub repository and the
branch (adapt the names):
```
git+https://github.com/ORGANIZATION/REPOSITORY.git@main
```

A corresponding `envionment.yml` file for conda would look like this (adapt the
names):
```yaml
name: experiment
channels:
  - conda-forge
dependencies:
  - python <= 3.12
  - pip
  - pip:
      - git+https://github.com/ORGANIZATION/REPOSITORY.git@main
```

Does it install and run? If yes, move on to the next step (test-PyPI and later
PyPI).


## Step 3: Deploy the package to test-PyPI using GitHub Actions

Our final step is to create a GitHub Actions workflow which will run when we
create a new release.

:::{danger}
I recommend to first practice this on the test-PyPI before deploying to the
real PyPI.
:::

Here is the workflow (`.github/workflows/package.yml`):
```yaml
name: Package

on:
  release:
    types: [created]

jobs:
  build:
    permissions: write-all
    runs-on: ubuntu-24.04

    steps:
    - name: Switch branch
      uses: actions/checkout@v4
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: "3.12"
    - name: Install Flit
      run: |
        pip install flit
    - name: Flit publish
      run:
        flit publish
      env:
        FLIT_USERNAME: __token__
        FLIT_PASSWORD: ${{ secrets.PYPI_TOKEN }}
        # uncomment the following line if you are using test.pypi.org:
#       FLIT_INDEX_URL: https://test.pypi.org/legacy/
        # this is how you can test the installation from test.pypi.org:
#       pip install --index-url https://test.pypi.org/simple/ package_name
```

About the `FLIT_PASSWORD: ${{ secrets.PYPI_TOKEN }}`:
- You obtain the token from PyPI by going to your account settings and
  creating a new token.
- You add the token to your GitHub repository as a secret (here with the name
  `PYPI_TOKEN`).
