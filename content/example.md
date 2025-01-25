# Example project: 2D classification task using a nearest-neighbor predictor

The [example code](https://github.com/workshop-material/classification-task)
that we will study is a relatively simple nearest-neighbor predictor written in
Python. It is not important or expected that we understand the code in detail.

The code will produce something like this:

:::{figure} img/chart.svg
:alt: Results of the classification task
:width: 100%

The bottom row shows the training data (two labels) and the top row shows the
test data and whether the nearest-neighbor predictor classified their labels
correctly.
:::

The **big picture** of the code is as follows:
- We can choose the number of samples (the example above has 50 samples).
- The code will generate samples with two labels (0 and 1) in a 2D space.
- One of the labels has a normal distribution and a circular distribution with
  some minimum and maximum radius.
- The second label only has a circular distribution with a different radius.
- Then we try to predict whether the test samples belong to label 0 or 1 based
  on the nearest neighbors in the training data. The number of neighbors can
  be adjusted and the code will take label of the majority of the neighbors.


## Example run

:::{instructor-note}
The instructor demonstrates running the code on their computer.
:::

The code is written to accept **command-line arguments** to specify the number
of samples and file names. Later we will discuss advantages of this approach.

Let us try to get the help text:
```console
$ python generate-data.py --help

Usage: generate-data.py [OPTIONS]

  Program that generates a set of training and test samples for a non-linear
  classification task.

Options:
  --num-samples INTEGER  Number of samples for each class.  [required]
  --training-data TEXT   Training data is written to this file.  [required]
  --test-data TEXT       Test data is written to this file.  [required]
  --help                 Show this message and exit.
```

We first generate the training and test data:
```console
$ python generate-data.py --num-samples 50 --training-data train.csv --test-data test.csv

Generated 50 training samples (train.csv) and test samples (test.csv).
```

In a second step we generate predictions for the test data:
```console
$ python generate-predictions.py --num-neighbors 7 --training-data train.csv --test-data test.csv --predictions predictions.csv

Predictions saved to predictions.csv
```

Finally, we can plot the results:
```console
$ python plot-results.py --training-data train.csv --predictions predictions.csv --output-chart chart.svg

Accuracy: 0.94
Saved chart to chart.svg
```


## Discussion and goals

:::{discussion}
- Together we look at the generated files (train.csv, test.csv, predictions.csv, chart.svg).
- We browse and discuss the [example code behind these scripts](https://github.com/workshop-material/classification-task).
:::

:::{admonition} Learning goals
- What are the most important steps to make this code **reusable by others**
  and **our future selves**?
- Be able to apply these techniques to your own code/script.
:::

:::{admonition} We will not focus on ...
- ... how the code works internally in detail.
- ... whether this is the most efficient algorithm.
- ... whether the code is numerically stable.
- ... how to code scales with system size.
- ... whether it is portable to other operating systems (we will discuss this later).
:::
