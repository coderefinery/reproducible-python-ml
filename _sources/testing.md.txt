# Automated testing

:::{objectives}
- Know **where to start** in your own project.
- Know what possibilities and techniques are available in the Python world.
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

**Do I even need testing?**:
- A simple script or notebook probably does not need an automated test.

**If you have nothing yet**:
- Start with an end-to-end test.
- Describe in words how *you* check whether the code still works.
- Translate the words into a script (any language).
- Run the script automatically on every code change (GitHub Actions or GitLab CI).

**If you want to start with unit-testing**:
- You want to rewrite a function? Start adding a unit test right there first.
- You spend few days chasing a bug? Once you fix it, add a test to make sure it does not come back.


## End-to-end tests

- This is our end-to-end test: <https://github.com/workshop-material/classification-task/blob/main/test.sh>
- Note how we can run it [on GitHub automatically](https://github.com/workshop-material/classification-task/blob/d5baee6a7600986b5fccc2fca4ee80a90c2d5f69/.github/workflows/test.yml#L28).
- Also browse <https://github.com/workshop-material/classification-task/actions>.
- If we have time, we can try to create a pull request which would break the
  code and see how the test fails.


## Pytest

Here is a simple example of a test:
```{code-block} python
---
emphasize-lines: 10-14
---
def fahrenheit_to_celsius(temp_f):
    """Converts temperature in Fahrenheit
    to Celsius.
    """
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c


# this is the test function
def test_fahrenheit_to_celsius():
    temp_c = fahrenheit_to_celsius(temp_f=100.0)
    expected_result = 37.777777
    # assert raises an error if the condition is not met
    assert abs(temp_c - expected_result) < 1.0e-6
```

To run the test(s):
```console
$ pytest example.py
```

Explanation: `pytest` will look for functions starting with `test_` in files
and directories given as arguments. It will run them and report the results.

Good practice to add unit tests:
- Add the test function and run it.
- Break the function on purpose and run the test.
- Does the test fail as expected?


## Adding the unit test to GitHub Actions

Our next goal is that we want GitHub to run the unit test
automatically on every change.

First we need to extend our
[environment.yml](https://github.com/workshop-material/classification-task/blob/main/environment.yml):
```{code-block} yaml
---
emphasize-lines: 12
---
name: classification-task
channels:
  - conda-forge
dependencies:
  - python <= 3.12
  - click
  - numpy
  - pandas
  - scipy
  - altair
  - vl-convert-python
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
    runs-on: ubuntu-24.04

    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - uses: mamba-org/setup-micromamba@v1
      with:
        micromamba-version: '2.0.5-0' # any version from https://github.com/mamba-org/micromamba-releases
        environment-file: environment.yml
        init-shell: bash
        cache-environment: true
        post-cleanup: 'all'
        generate-run-shell: false

    - name: Run tests
      run: |
        ./test.sh
        pytest generate-predictions.py
      shell: bash -el {0}
```

In the above example, we assume that we added a test function to `generate-predictions.py`.

If we have time, we can try to create a pull request which would break the
code and see how the test fails.


## What else is possible

- Run the test set **automatically** on every code change:
  - [GitHub Actions](https://github.com/features/actions)
  - [GitLab CI](https://docs.gitlab.com/ee/ci/)

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

:::{exercise}
Experiment with the example project and what we learned above or try it **on
the example project or on your own project**:
- Add a unit test. **If you are unsure where to start**, you can try to move
  [the majority
  vote](https://github.com/workshop-material/classification-task/blob/79ce3be8fc187afbc33c91c11ea7003ce9bf56cd/generate_predictions.py#L28)
  into a separate function and write a test function for it.
- Try to run pytest locally.
- Check whether it fails when you break the corresponding function.
- Try to run it on GitHub Actions.
- Create a pull request which would break the code and see whether the automatic test would catch it.
- Try to design an end-to-end test for your project. Already the thought
  process can be very helpful.
:::
