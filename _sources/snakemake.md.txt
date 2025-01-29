# How to parallelize independent tasks using workflows (example: [Snakemake](https://snakemake.github.io/))

:::{objectives}
- Understand the concept of a workflow management tool.
- Instead of thinking in terms of individual step-by-step commands, think in
  terms of **dependencies** (**rules**).
- Try to port our computational pipeline to Snakemake.
- See how Snakemake can identify independent steps and run them in parallel.
- It is not our goal to remember all the details of Snakemake.
:::


## The problem

Imagine we want to process a large number of similar input data.

This could be one way to do it:
```bash
#!/usr/bin/env bash

num_rounds=10

for i in $(seq -w 1 ${num_rounds}); do
    python generate_data.py \
            --num-samples 2000 \
            --training-data data/train_${i}.csv \
            --test-data data/test_${i}.csv

    python generate_predictions.py \
            --num-neighbors 7 \
            --training-data data/train_${i}.csv \
            --test-data data/test_${i}.csv
            --predictions results/predictions_${i}.csv

    python plot_results.py \
            --training-data data/train_${i}.csv \
            --predictions results/predictions_${i}.csv \
            --output-chart results/chart_${i}.png
done
```

Discuss possible problems with this approach.


## Thinking in terms of dependencies

For the following we will assume that we have the input data available:
```bash
#!/usr/bin/env bash

num_rounds=10

for i in $(seq -w 1 ${num_rounds}); do
    python generate_data.py \
            --num-samples 2000 \
            --training-data data/train_${i}.csv \
            --test-data data/test_${i}.csv
done
```

From here on we will **focus on the processing part**.

The central file in Snakemake is the `snakefile`. This is how we can express
the pipeline in Snakemake (below we will explain it):
```
# the comma is there because glob_wildcards returns a named tuple
numbers, = glob_wildcards("data/train_{number}.csv")


# rule that collects the target files
rule all:
    input:
        expand("results/chart_{number}.svg", number=numbers)


rule chart:
    input:
        script="plot_results.py",
        predictions="results/predictions_{number}.csv",
        training="data/train_{number}.csv"
    output:
        "results/chart_{number}.svg"
    log:
        "logs/chart_{number}.txt"
    shell:
        """
        python {input.script} --training-data {input.training} --predictions {input.predictions} --output-chart {output}
        """


rule predictions:
    input:
        script="generate_predictions.py",
        training="data/train_{number}.csv",
        test="data/test_{number}.csv"
    output:
        "results/predictions_{number}.csv"
    log:
        "logs/predictions_{number}.txt"
    shell:
        """
        python {input.script} --num-neighbors 7 --training-data {input.training} --test-data {input.test} --predictions {output}
        """
```

**Explanation**:
- The `snakefile` contains 3 **rules** and it will run the "all" rule by default unless
  we ask it to produce a different "target":
  - "all"
  - "chart"
  - "predictions"
- Rules "predictions" and "chart" depend on **input** and produce **output**.
- Note how "all" depends on the output of the "chart" rule and how "chart" depends
  on the output of the "predictions" rule.
- The **shell** part of the rule shows how to produce the output from the
  input.
- We ask Snakemake to collect all files that match `"data/train_{number}.csv"`
  and from this to infer the **wildcards** `{number}`.
- Later we can refer to `{number}` throughout the `snakefile`.
- This part defines what we want to have at the end:
  ```
  rule all:
      input:
          expand("results/chart_{number}.svg", number=numbers)
  ```
- Rules correspond to steps and parameter scanning can be done with wildcards.


## Exercise

::::{exercise} Exercise: Practicing with Snakemake
1. Create a `snakefile` (above) and run it with Snakemake (adjust number of
   cores):
   ```console
   $ snakemake --cores 8
   ```

1. Check the output. Did it use all available cores? How did it know
   which steps it can start in parallel?

1. Run Snakemake again. Now it should finish almost immediately because all the
   results are already there. Aha! Snakemake does not repeat steps that are
   already done.  You can force it to re-run all with `snakemake
   --delete-all-output`.

1. Remove few files from `results/` and run it again.
   Snakemake should now only re-run the steps that are necessary to get the
   deleted files.

1. Modify `generate_predictions.py` which is used in the rule "predictions".
   Now Snakemake will only re-run the steps that depend on this script.

1. It is possible to only process one file with (useful for testing):
   ```console
   $ snakemake results/predictions_09.csv
   ```

1. Add few more data files to the input directory `data/` (for instance by
   copying some existing ones) and observe how Snakemake will pick them up next
   time you run the workflow, without changing the `snakefile`.
::::


## What else is possible?

- With the option `--keep-going` we can tell Snakemake to not give up on first failure.

- The option `--restart-times 3` would tell Snakemake to try to restart a rule
  up to 3 times if it fails.

- It is possible to tell Snakemake to use a **locally mounted file system** instead
  of the default network file system for certain rules
  ([documentation](https://snakemake.github.io/snakemake-plugin-catalog/plugins/storage/fs.html)).

- Sometimes you need to run different rules inside different software
  environments (e.g. **Conda environments**) and this is possible.

- A lot **more is possible**:
  - [Snakemake documentation](https://snakemake.readthedocs.io)
  - [Snakemake tutorial](https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html)


## More elaborate example

In this example below we also scan over a range of numbers for the `--num-neighbors` parameter:
:::{code-block}
:emphasize-lines: 7,40-41


# the comma is there because glob_wildcards returns a named tuple
numbers, = glob_wildcards("data/train_{number}.csv")


# define the parameter scan for num-neighbors
neighbor_values = [1, 3, 5, 7, 9, 11]


# rule that collects all target files
rule all:
    input:
        expand("results/chart_{number}_{num_neighbors}.svg", number=numbers, num_neighbors=neighbor_values)


rule chart:
    input:
        script="plot_results.py",
        predictions="results/predictions_{number}_{num_neighbors}.csv",
        training="data/train_{number}.csv"
    output:
        "results/chart_{number}_{num_neighbors}.svg"
    log:
        "logs/chart_{number}_{num_neighbors}.txt"
    shell:
        """
        python {input.script} --training-data {input.training} --predictions {input.predictions} --output-chart {output}
        """


rule predictions:
    input:
        script="generate_predictions.py",
        training="data/train_{number}.csv",
        test="data/test_{number}.csv"
    output:
        "results/predictions_{number}_{num_neighbors}.csv"
    log:
        "logs/predictions_{number}_{num_neighbors}.txt"
    params:
        num_neighbors=lambda wildcards: wildcards.num_neighbors
    shell:
        """
        python {input.script} --num-neighbors {params.num_neighbors} --training-data {input.training} --test-data {input.test} --predictions {output}
        """
:::


## Other workflow management tools

- Another very popular one is [Nextflow](https://www.nextflow.io/).

- Many workflow management tools exist
  ([overview](https://github.com/common-workflow-language/common-workflow-language/wiki/Existing-Workflow-systems)).
