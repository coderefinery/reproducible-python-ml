# Automated testing

:::{objectives}
- Know **where to start** in your own project.
- Have an example for how to make the **testing part of code review**.
:::

:::{instructor-note}
- (15 min) Motivation
- (15 min) End-to-end tests
- (15 min) Pytest
- (15 min) Adding the unit test to GitHub Actions
- (10 min) What else is possible
- (20 min) Exercise
:::


## Motivation

Testing is a way to check that the code does what it is expected to.

- **Less scary to change code**: tests will tell you whether something broke.
- **Easier for new people** to join.
- Easier for somebody to **revive an old code**.
- **End-to-end test**: run the whole code and compare result to a reference.
- **Unit tests**: test one unit (function or module). Can guide towards better
  structured code: complicated code is more difficult to test.


## How testing is often taught

```python
def add(a, b):
    return a + b


def test_add():
    assert add(1, 2) == 3
```

How this feels:
:::{figure} img/owl.png
:alt: Instruction on how to draw an owl
:width: 50%
:class: with-border

[Citation needed]
:::

Instead, we will look at and **discuss a real example** where we test components
from our example project.


## Where to start

Short answer: **Start with an end-to-end test**.

:::{solution} Longer answer
- A simple script or notebook probably does not need an automated test.

**If you have nothing yet**:
- Start with an end-to-end test.
- Describe in words how *you* check whether the code still works.
- Translate the words into a script (any language).
- Run the script automatically on every code change.

**If you want to start with unit-testing**:
- You want to rewrite a function? Start adding a unit test right there first.
:::


## End-to-end tests

- This is our end-to-end test: <https://github.com/workshop-material/planets/blob/main/test.sh>
- Note how we can run it [on GitHub automatically](https://github.com/workshop-material/planets/blob/813d49a247f36e9c1e10cbe78ecf1ae4b6e971c3/.github/workflows/test.yml#L28).
- Also browse <https://github.com/workshop-material/planets/actions>.
- If we have time, we can try to create a pull request which would break the
  code and see how the test fails.

:::{discussion}
Is the [end-to-end test](https://github.com/workshop-material/planets/blob/main/test.sh)
perfect? No. But it's a good starting point. Discuss its limitations.
:::


## Pytest

First we need to add a test function, for instance
for [this function](https://github.com/workshop-material/planets/blob/813d49a247f36e9c1e10cbe78ecf1ae4b6e971c3/simulate.py#L31-L39):
```{code-block} python
---
emphasize-lines: 12-20
---
def force_between_planets(position1, mass1, position2, mass2):
    G = 1.0  # gravitational constant

    r = position2 - position1
    distance = (r[0] ** 2 + r[1] ** 2 + r[2] ** 2) ** 0.5
    force_magnitude = G * mass1 * mass2 / distance**2
    force = (r / distance) * force_magnitude

    return force


def test_force_between_planets():
    position1 = np.array([0.0, 0.0, 0.0])
    mass1 = 1.0
    position2 = np.array([1.0, 0.0, 0.0])
    mass2 = 2.0

    force = force_between_planets(position1, mass1, position2, mass2)

    assert np.allclose(force, [2.0, 0.0, 0.0])
```

Let us run the test with:
```console
$ pytest simulate.py
```

Explanation: `pytest` will look for functions starting with `test_` in files
and directories given as arguments. It will run them and report the results.

Now let us try this:
- Commit the test.
- Break the function on purpose and run the test.
- Does the test fail as expected?


## Adding the unit test to GitHub Actions

Our next goal is that we want GitHub to run the unit test
automatically on every change.

First we need to extend our
[environment.yml](https://github.com/workshop-material/planets/blob/main/environment.yml):
```{code-block} yaml
---
emphasize-lines: 9
---
name: planets
channels:
  - conda-forge
dependencies:
  - python=3.12
  - numpy
  - click
  - matplotlib
  - pytest
```

We also need to extend `.github/workflows/test.yml` (highlighted line):
```{code-block} yaml
---
emphasize-lines: 29
---
name: Test

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
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

    - name: Run tests
      run: |
        ./test.sh
        pytest simulate.py
      shell: bash -el {0}
```

If we have time, we can try to create a pull request which would break the
code and see how the test fails.


## What else is possible

- The testing above used **example-based** testing.

- **Test coverage**: how much of the code is traversed by tests?
  - Python: [pytest-cov](https://pytest-cov.readthedocs.io/)
  - Result can be deployed to services like [Codecov](https://about.codecov.io/) or [Coveralls](https://coveralls.io/).

- **Property-based** testing: generates arbitrary data matching your specification and checks that your guarantee still holds in that case.
  - Python: [hypothesis](https://hypothesis.readthedocs.io/)

- **Snapshot-based** testing: makes it easier to generate snapshots for regression tests.
  - Python: [syrupy](https://syrupy-project.github.io/syrupy/)

- **Mutation testing**: tests pass -> change a line of code (make a mutant) -> test again and check whether all mutants get "killed".
  - Python: [mutmut](https://mutmut.readthedocs.io/)


## Exercises

Experiment with the example project and what we learned above or try it on your
own project:
- Add a unit test.
- Try to run it locally.
- Check whether it fails when you break the corresponding function.
- Try to run it on GitHub Actions.
- Create a pull request which would break the code and see whether the automatic test would catch it.
- Try to design an end-to-end test for your project.
