# Conflict resolution


## Resolving a conflict (demonstration)

A conflict is when Git asks humans to decide during a merge which of two
changes to keep **if the same portion of a file has been changed in two
different ways on two different branches**.

We will practice conflict resolution in the collaborative Git lesson (next
day).

Here we will only demonstrate how to create a conflict and how to resolve it,
**all on GitHub**. Once we understand how this works, we will be more confident
to resolve conflicts also in the **command line** (we can demonstrate this if
we have time).

How to create a conflict (please try this in your own time *and just watch now*):
- Create a new branch from `main` and on it make a change to a file.
- On `main`, make a different change to the same part of the same file.
- Now try to merge the new branch to `main`. You will get a conflict.

How to resolve conflicts:
- On GitHub, you can resolve conflicts by clicking on the "Resolve conflicts"
  button. This will open a text editor where you can choose which changes to
  keep.
  Make sure to remove the conflict markers.
  After resolving the conflict, you can commit the changes and merge the
  pull request.
- Sometimes a conflict is between your change and somebody else's change. In
  that case, you might have to discuss with the other person which changes to
  keep.


## Avoiding conflicts

```{discussion} The human side of conflicts
- What does it mean if two people do the same thing in two different ways?
- What if you work on the same file but do two different things in the different sections?
- What if you do something, don't tell someone from 6 months, and then try to combine it with other people's work?
- How are conflicts avoided in other work? (Only one person working at once?
  Declaring what you are doing before you start, if there is any chance someone
  else might do the same thing, helps.)
```

- Human measures
  - Think and plan to which branch you will commit to.
  - Do not put unrelated changes on the same branch.
- Collaboration measures
  - Open an issue and discuss with collaborators before starting a long-living
    branch.
- Project layout measures
  - Modifying global data often causes conflicts.
  - Modular programming reduces this risk.
- Technical measures
  - **Share your changes early and often**: This is one of the happy,
    rare circumstances when everyone doing the selfish thing (publishing your
    changes as early as practical) results in best case for everyone!
  - Pull/rebase often to keep up to date with upstream.
  - Resolve conflicts early.
