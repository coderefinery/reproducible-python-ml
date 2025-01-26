---
orphan: true
---

# Demo: From a script towards a workflow

In this episode we will explore code quality and good practices in Python using
a hands-on approach. We will together build up a small project and improve it
step by step.

We will start from a relatively simple image processing script which can read a
telescope image of stars and our goal is to **count the number of stars** in
the image. Later we will want to be able to process many such images.

The (fictional) telescope images look like the one below here ([in this
repository](https://github.com/workshop-material/random-star-images) we can find more):
:::{figure} refactoring/stars.png
:alt: Generated image representing a telescope image of stars
:width: 60%

Generated image representing a telescope image of stars.
:::

:::{admonition} Rough plan for this demo
- (15 min) Discuss how we would solve the problem, run example code, and make it work (as part of a Jupyter notebook)?
- (15 min) Refactor the positioning code into a function and a module
- (15 min) Now we wish to process many images - discuss how we would approach this
- (15 min) Introduce CLI and discuss the benefits
- (30 min) From a script to a workflow (using Snakemake)
:::

:::{solution} Starting point (spoiler alert)

We can imagine that we pieced together the following code
based on some examples we found online:
```python
import matplotlib.pyplot as plt
from skimage import io, filters, color
from skimage.measure import label, regionprops


image = io.imread("stars.png")
sigma = 0.5

# if there is a fourth channel (alpha channel), ignore it
rgb_image = image[:, :, :3]
gray_image = color.rgb2gray(rgb_image)

# apply a gaussian filter to reduce noise
image_smooth = filters.gaussian(gray_image, sigma)

# threshold the image to create a binary image (bright stars will be white, background black)
thresh = filters.threshold_otsu(image_smooth)
binary_image = image_smooth > thresh

# label connected regions (stars) in the binary image
labeled_image = label(binary_image)

# get properties of labeled regions
regions = regionprops(labeled_image)

# extract star positions (centroids)
star_positions = [region.centroid for region in regions]

# plot the original image
plt.figure(figsize=(8, 8))
plt.imshow(image, cmap="gray")

# overlay star positions with crosses
for star in star_positions:
    plt.plot(star[1], star[0], "rx", markersize=5, markeredgewidth=0.1)

plt.savefig("detected-stars.png", dpi=300)

print(f"number of stars detected: {len(star_positions)}")
```
:::


## Plan

Topics we wish to show and discuss:
- Naming (and other) conventions, project organization, modularity
- The value of pure functions and immutability
- Refactoring (explained through examples)
- Auto-formatting and linting with tools like black, vulture, ruff
- Moving a project under Git
- How to document dependencies
- Structuring larger software projects in a modular way
- Command-line interfaces
- Workflows with Snakemake

We will work together on the code on the big screen, and participants will be
encouraged to give suggestions and ask questions.  We will **end up with a Git
repository** which will be shared with workshop participants.


## Possible solutions

:::{solution} Script after some work, with command-line interface (spoiler alert)
This is one possible solution (`countstars.py`):
```{literalinclude} refactoring/countstars.py
:language: python
```
:::

:::{solution} Snakemake rules which define a workflow (spoiler alert)
This is one possible solution (`snakefile`):
```{literalinclude} refactoring/snakefile
:language: python
```

We can process as many images as we like by running:
```console
$ snakemake --cores 4  # adjust to the number of available cores
```
:::
