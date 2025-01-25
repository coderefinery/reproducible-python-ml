(documentation)=

# Code documentation

:::{objectives}
- Discuss what makes good documentation.
- Improve the README of your project or our example project.
- Explore Sphinx which is a popular tool to build documentation websites.
- Learn how to leverage GitHub Actions and GitHub Pages to build and deploy documentation.
:::

:::{instructor-note}
- (30 min) Discussion
- (30 min) Exercise: Set up a Sphinx documentation and add API documentation
- (15 min) Demo: Building documentation with GitHub Actions
:::


## Why? &#128151;&#9993;&#65039; to your future self

- You will probably use your code in the future and may forget details.
- You may want others to use your code or contribute
  (almost impossible without documentation).


## In-code documentation

Not very useful (more commentary than comment):
```python
# now we check if temperature is below -50
if temperature < -50:
    print("ERROR: temperature is too low")
```

More useful (explaining **why**):
```python
# we regard temperatures below -50 degrees as measurement errors
if temperature < -50:
    print("ERROR: temperature is too low")
```

Keeping zombie code "just in case" (rather use version control):
```python
# do not run this code!
# if temperature > 0:
#     print("It is warm")
```

Emulating version control:
```python
# John Doe: threshold changed from 0 to 15 on August 5, 2013
if temperature > 15:
    print("It is warm")
```


## Many languages allow "docstrings"

Example (Python):
```python
def kelvin_to_celsius(temp_k: float) -> float:
    """
    Converts temperature in Kelvin to Celsius.

    Parameters
    ----------
    temp_k : float
        temperature in Kelvin

    Returns
    -------
    temp_c : float
        temperature in Celsius
    """
    assert temp_k >= 0.0, "ERROR: negative T_K"

    temp_c = temp_k - 273.15

    return temp_c
```

:::{keypoints}
- Documentation which is only in the source code is not enough.
- Often a README is enough.
- Documentation needs to be kept
  **in the same Git repository** as the code since we want it to evolve with
  the code.
:::


## Often a README is enough - checklist

- **Purpose**
- Requirements
- Installation instructions
- **Copy-paste-able example to get started**
- Tutorials covering key functionality
- Reference documentation (e.g. API) covering all functionality
- Authors and **recommended citation**
- License
- Contribution guide

See also the
[JOSS review checklist](https://joss.readthedocs.io/en/latest/review_checklist.html).


## Diátaxis

Diátaxis is a systematic approach to technical documentation authoring.

- Overview: <https://diataxis.fr/>
- How to use Diátaxis **as a guide** to work: <https://diataxis.fr/how-to-use-diataxis/>


## What if you need more than a README?

- Write documentation in
  [Markdown (.md)](https://en.wikipedia.org/wiki/Markdown)
  or
  [reStructuredText (.rst)](https://en.wikipedia.org/wiki/ReStructuredText)
  or
  [R Markdown (.Rmd)](https://rmarkdown.rstudio.com/)

- In the **same repository** as the code -> version control and **reproducibility**

- Use one of many tools to build HTML out of md/rst/Rmd:
  [Sphinx](https://sphinx-doc.org),
  [MkDocs](https://www.mkdocs.org/),
  [Zola](https://www.getzola.org/), [Jekyll](https://jekyllrb.com/),
  [Hugo](https://gohugo.io/), RStudio, [knitr](https://yihui.org/knitr/),
  [bookdown](https://bookdown.org/),
  [blogdown](https://bookdown.org/yihui/blogdown/), ...

- Deploy the generated HTML to [GitHub Pages](https://pages.github.com/) or
  [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/)


## Exercise: Set up a Sphinx documentation

:::{prereq} Preparation
In this episode we will use the following 5 packages which we installed
previously as part of the {doc}`installation`:
```
myst-parser
sphinx
sphinx-rtd-theme
sphinx-autoapi
sphinx-autobuild
```

Which repository to use? You have 3 options:
- Clone **your fork** of the planets example repository.
- If you don't have that, you can clone the original repository itself:
  <https://github.com/workshop-material/planets>
- You can try this with **your own project** and the project does not have to
  be a Python project.
:::

There are at least two ways to get started with Sphinx:
1. Use `sphinx-quickstart` to create a new Sphinx project.
1. **This is what we will do instead**: Create three files (`doc/conf.py`, `doc/index.md`, and `doc/about.md`)
   as starting point and improve from there.

::::{exercise} Exercise: Set up a Sphinx documentation
1. Create the following three files in your project:
   ```
   planets/      <- or your own project
   ├── doc/
   │   ├── conf.py
   │   ├── index.md
   │   └── about.md
   └── ...
   ```

   This is `conf.py`:
   ```python
   project = "planets"
   copyright = "2024, Authors"
   author = "Authors"
   release = "0.1"

   exclude_patterns = ["_build", "Thumbs.db", ".DS_Store"]

   extensions = [
       "myst_parser",  # in order to use markdown
   ]

   myst_enable_extensions = [
       "colon_fence",  # ::: can be used instead of ``` for better rendering
   ]

   html_theme = "sphinx_rtd_theme"
   ```

   This is `index.md` (feel free to change the example text):
   ```markdown
   # Our code documentation

   Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
   incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
   nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
   Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
   fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
   culpa qui officia deserunt mollit anim id est laborum.

   :::{toctree}
   :maxdepth: 2
   :caption: Some caption

   about.md
   :::
   ```

   This is `about.md` (feel free to adjust):
   ```markdown
   # About this code

   Work in progress ...
   ```

1. Run `sphinx-build` to build the HTML documentation:
   ```console
   $ sphinx-build doc _build

   ... lots of output ...
   The HTML pages are in _build.
   ```

1. Try to open `_build/index.html` in your browser.

1. Experiment with adding more content, images, equations, code blocks, ...
   - [typography](https://myst-parser.readthedocs.io/en/latest/syntax/typography.html)
   - [images](https://myst-parser.readthedocs.io/en/latest/syntax/images_and_figures.html)
   - [math and equations](https://myst-parser.readthedocs.io/en/latest/syntax/math.html)
   - [code blocks](https://myst-parser.readthedocs.io/en/latest/syntax/code_and_apis.html)
::::

There is a lot more you can do:
- This is useful if you want to check the integrity of all internal and external links:
  ```console
  $ sphinx-build doc -W -b linkcheck _build
  ```
- [sphinx-autobuild](https://pypi.org/project/sphinx-autobuild/)
  provides a local web server that will automatically refresh your view
  every time you save a file - which makes writing with live-preview much easier.


## Demo: Building documentation with GitHub Actions

:::{instructor-note}
- Instructor presents.
- Learners are encouraged to try this later on their own.
:::

First we need to extend the `environment.yml` file to include the necessary packages:
```{code-block} yaml
---
emphasize-lines: 9-12
---
name: planets
channels:
  - conda-forge
dependencies:
  - python=3.12
  - numpy
  - click
  - matplotlib
  - myst-parser
  - sphinx
  - sphinx-rtd-theme
  - sphinx-autoapi
```

Then we add a GitHub Actions workflow `.github/workflow/sphinx.yml` to build the documentation:
```{code-block} yaml
---
emphasize-lines: 31
---
name: Build documentation

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

permissions:
  contents: write

jobs:
  docs:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - uses: mamba-org/setup-micromamba@v1
      with:
        micromamba-version: '1.5.8-0' # any version from https://github.com/mamba-org/micromamba-releases
        environment-file: environment.yml
        init-shell: bash
        cache-environment: true
        post-cleanup: 'all'
        generate-run-shell: false

    - name: Sphinx build
      run: |
        sphinx-build doc _build
      shell: bash -el {0}

    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v4
      if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}
      with:
        publish_branch: gh-pages
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: _build/
        force_orphan: true
```

Now:
- Add these two changes to the GitHub repository.
- Go to "Settings" -> "Pages" -> "Branch" -> `gh-pages` -> "Save".
- Look at "Actions" tab and observe the workflow running and hopefully
  deploying the website.
- Finally visit the generated site. You can find it by clicking the About wheel
  icon on top right of your repository. There, select "Use your GitHub Pages
  website".
- **This is how we build almost all of our lesson websites**,
  including this one!
- Another popular place to deploy Sphinx documentation is [ReadTheDocs](https://readthedocs.org/).


## Optional: How to auto-generate API documentation in Python

Add three tiny modifications (highlighted) to `doc/conf.py` to auto-generate API documentation
(this requires the `sphinx-autoapi` package):
```{code-block} python
---
emphasize-lines: 10, 14, 17
---
project = "planets"
copyright = "2024, Authors"
author = "Authors"
release = "0.1"

exclude_patterns = ["_build", "Thumbs.db", ".DS_Store"]

extensions = [
    "myst_parser",  # in order to use markdown
    "autoapi.extension",  # in order to use markdown
]

# search this directory for Python files
autoapi_dirs = [".."]

# ignore this file when generating API documentation
autoapi_ignore = ["*/conf.py"]

myst_enable_extensions = [
    "colon_fence",  # ::: can be used instead of ``` for better rendering
]

html_theme = "sphinx_rtd_theme"
```

Then rebuild the documentation (or push the changes and let GitHub rebuild it)
and you should see a new section "API Reference".


## Confused about reStructuredText vs. Markdown vs. MyST?

- At the beginning there was reStructuredText and Sphinx was built for reStructuredText.
- Independently, Markdown was invented and evolved into a couple of flavors.
- Markdown became more and more popular but was limited compared to reStructuredText.
- Later, [MyST](https://myst-parser.readthedocs.io/en/latest/syntax/typography.html)
  was invented to be able to write
  something that looks like Markdown but in addition can do everything that
  reStructuredText can do with extra directives.


## Where to read more

- [CodeRefinery documentation lesson](https://coderefinery.github.io/documentation/)
- [Sphinx documentation](https://www.sphinx-doc.org/)
- [Sphinx + ReadTheDocs guide](https://sphinx-rtd-tutorial.readthedocs.io/en/latest/index.html)
- For more Markdown functionality, see the [Markdown guide](https://www.markdownguide.org/basic-syntax/).
- For Sphinx additions, see [Sphinx Markup Constructs](https://www.sphinx-doc.org/en/master/markup/index.html).
- [An opinionated guide on documentation in Python](https://docs.python-guide.org/writing/documentation/)
