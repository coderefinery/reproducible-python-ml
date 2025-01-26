# Choosing a software license

:::{objectives}
- Knowing about what derivative work is and whether we can share it.
- Get familiar with terminology around licensing.
- We will add a license to our example project.
:::


## Copyright and derivative work: Sampling/remixing

:::{figure} img/ai/record-player.png
:alt: Generated image of a monk operating a record player
:width: 50%
:::
[Midjourney, CC-BY-NC 4.0]

:::{figure} img/ai/turntable.png
:alt: Generated image of a monk operating two record players
:width: 50%
:::
[Midjourney, CC-BY-NC 4.0]

- Copyright controls whether and how we can distribute
  the original work or the **derivative work**.
- In the **context of software** it is more about
  being able to change and **distribute changes**.
- Changing and distributing software is similar to changing and distributing
  music
- You can do almost anything if you don't distribute it

**Often we don't have the choice**:
- We are expected to publish software
- Sharing can be good insurance against being locked out

**Can we distribute our changes** with the research community or our future selves?


## Why software licenses matter

You find some great code that you want to reuse for your own publication.

- This is good for the original author - you will cite them. Maybe other people who cite you will cite them.

- You modify and remix the code.

- Two years later ... &#8987;

- Time to publish: You realize **there is no license to the original work** &#128561;

**Now we have a problem**:
- &#128556; "Best" case: You manage to publish the paper without the software/data.
  Others cannot build on your software and data.
- &#128561; Worst case: You cannot publish it at all.
  Journal requires that papers should come with data and software so that they are reproducible.


## Taxonomy of software licenses

:::{figure} img/license-models.png
:alt: "European Union Public Licence (EUPL): guidelines July 2021"

European Commission, Directorate-General for Informatics, Schmitz, P., European Union Public Licence (EUPL): guidelines July 2021, Publications Office, 2021, <https://data.europa.eu/doi/10.2799/77160>
:::

Comments:
- Arrows represent compatibility (A -> B: B can reuse A)
- Proprietary/custom: Derivative work typically not possible (no arrow goes from proprietary to open)
- Permissive: Derivative work does not have to be shared
- Copyleft/reciprocal: Derivative work must be made available under the same license terms
- NC (non-commercial) and ND (non-derivative) exist for data licenses but not really for software licenses

**Great resource for comparing software licenses**: [Joinup Licensing Assistant](https://joinup.ec.europa.eu/collection/eupl/solution/joinup-licensing-assistant/jla-find-and-compare-software-licenses)
- Provides comments on licenses
- Easy to compare licenses ([example](https://joinup.ec.europa.eu/licence/compare/BSD-3-Clause;Apache-2.0))
- [Joinup Licensing Assistant - Compatibility Checker](https://joinup.ec.europa.eu/collection/eupl/solution/joinup-licensing-assistant/jla-compatibility-checker)
- Not biased by some company agenda


## Exercise/demo

:::{exercise}
- Let us choose a license for our example project.
- We will add a LICENSE to the repository.
:::

:::{discussion}
- What if my code uses libraries like `scikit-image`, `scikit-learn`, `numpy`,
  `matplotlib`, etc. Do we need to look at their licenses? In other words,
  **is our project derivative work** of something else?
:::


## More resources

- Presentation slides "Practical software licensing" (R. Bast): <https://doi.org/10.5281/zenodo.11554001>
- [Social coding lesson material](https://coderefinery.github.io/social-coding/)
- [UiT research software licensing guide (draft)](https://research-software.uit.no/blog/2023-software-licensing-guide/)
- [Research institution policies to support research software (compiled by the Research Software Alliance)](https://www.researchsoft.org/software-policies/)
- More [reading material](https://coderefinery.github.io/social-coding/software-licensing/#great-resources)


## More exercises

:::{exercise} Exercise: What constitutes derivative work?

Which of these are derivative works?  Also reflect/discuss how this affects the
choice of license.
- A. Download some code from a website and add on to it
- B. Download some code and use one of the functions in your code
- C. Changing code you got from somewhere
- D. Extending code you got from somewhere
- E. Completely rewriting code you got from somewhere
- F. Rewriting code to a different programming language
- G. Linking to libraries (static or dynamic), plug-ins, and drivers
- H. Clean room design (somebody explains you the code but you have never seen it)
- I. You read a paper, understand algorithm, write own code

```{solution}
- Derivative work: A-F
- Not derivative work: G-I
- E and F: This depends on how you do it, see "clean room design".
```
:::

:::{exercise} Exercise: Licensing situations

Consider some common licensing situations. If you are part of an exercise
group, discuss these with others:
1. What is the StackOverflow license for code you copy and paste?
2. A journal requests that you release your software during publication. You have
   copied a portion of the code from another package, which you have forgotten.
   Can you satisfy the journal's request?
3. You want to fix a bug in a project someone else has released, but there is no license. What risks are there?
4. How would you ask someone to add a license?
5. You incorporate MIT, GPL, and BSD3 licensed code into your project. What possible licenses can you pick for your project?
6. You do the same as above but add in another license that looks strong copyleft. What possible licenses can you use now?
7. Do licenses apply if you don't distribute your code? Why or why not?
8. Which licenses are most/least attractive for companies with proprietary software?

```{solution}
1. As indicated [here](https://stackoverflow.com/help/licensing), all publicly accessible user contributions are licensed under [Creative Commons Attribution-ShareAlike](https://creativecommons.org/licenses/by-sa/4.0/) license. See Stackoverflow [Terms of service](https://stackoverflow.com/legal/terms-of-service/public#licensing) for more detailed information.
2. "Standard" licensing rules apply. So in this case, you would need to remove the portion of code you have copied from another package before being able to release your software.
3. By default you are no authorized to use the content of a repository when there is no license. And derivative work is also not possible by default. Other risks: it may not be clear whether you can use and distribute (publish) the bugfixed code. For the repo owners it may not be clear whether they can use and distributed the bugfixed code. However, the authors may have forgotten to add a license so we suggest you to contact the authors (e.g. make an issue) and ask whether they are willing to add a license.
4. As mentionned in 3., the easiest is to fill an issue and explain the reasons why you would like to use this software (or update it).
5. Combining software with different licenses can be tricky and it is important to understand compatibilities (or lack of compatibilities) of the various licenses. GPL license is the most protective (BSD and MIT are quite permissive) so for the resulting combined software you could use a GPL license. However, re-licensing may not be necessary.
6. Derivative work would need to be shared under this strong copyleft license (e.g. AGPL or GPL), unless the components are only plugins or libraries.
7. If you keep your code for yourself, you may think you do not need a license. However, remember that in most companies/universities, your employer is "owning" your work and when you leave you may not be allowed to "distribute your code to your future self". So the best is always to add a license!
8. The least attractive licenses for companies with proprietary software are licenses where you would need to keep an open license when creating derivative work. For instance GPL and and AGPL. The most attractive licenses are permissive licenses where they can reuse, modify and relicense with no conditions. For instance MIT, BSD and Apache License.
```
:::
