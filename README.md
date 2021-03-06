# Species choice analysis

The species choice analysis is about hedging bets on which species will successfully form a functioning and persistent coral reef in the future. The aim is to construct an objective analytical framework for selecting of *n* species to focus on for restoration or other forms of preservation. There are two key components of the framework. The first is selecting a broad range of life histories using trait space as our template. This step is important because there are physiological and demographic trade-offs among species. Species good at one life history strategy (e.g., producing carbonate quickly) tend to be poor at others (e.g., surviving storms or reproducing). The second key component is prioritising species with qualities that have are known to help them persist in uncertain future environments. For instance, species with higher local abundances and larger geographic range sizes tend to recovery faster from disturbances, and also have more genetic diversity for evolution in novel conditions via selection, because genetic drift is less pervasive. Additionally, species that are evolutionarily older may also be expected to deal with change better because they're done it before; although, older species have also been shown to be more prone to extinction in analyses of marine fauna in Phanerozoic fossil records.

So, we hedge our bet by:

1. Selecting an *even* range of functionally important traits, including morphology, physiology and demography.
2. Weighing certains species more-so based on regional abundance, geographic range size, and extinction survival.

In doing so, we hope to capture high levels of genetic and phylogenetic diversity, and therefore a range of sensitivities to future stressors.

## Analysis

Here are the 394 species we consider: [species.csv](output/species.csv)

### Step 1: Trait space

We used trait data from [this paper](https://www.pnas.org/content/115/12/3084.short), which includes numerical (1-5) trait values for all species. The data is available [here](https://research.jcu.edu.au/researchdata/default/detail/2d343a3dc21a6a25831f3fbaa508efa7/). The traits are selected to represent the functional importance of corals. They are:

- Growth rate (GR)
- Corallite width (CW)
- Rugosity/branch spacing (R)
- Surface area per unit volume (SAV)
- Colony height (CH)
- Maximum colony size/diameter (MCS)
- Skeletal density (SD)

Figure 3 of the original paper shows that a PCoA (principal coordinates analysis) of these traits separates out the major morphological groups, and that the GBR has different occupancy to the Caribbean due to the lack of branching corals. Each point is a species and the contours show dense clusters:

<p align="center">
<img src="figs/pnas.png" alt="drawing" width="400"/> </p>
<br/>

The trait vectors indicate the areas of trait space that bring high trait values. The axes reflect trade-offs, e.g. between growth and corallite size on axis 1, which captures a range of demographic and physiological variation, and height and skeletal density/surface area on axis 2:

<p align="center">
<img src="figs/vectors.png" alt="drawing" width="400"/> </p>

### Step 2: Even spread in trait space

To select species (points) with maximum spread in trait space we used [voronoi mosaics](https://en.wikipedia.org/wiki/Voronoi_diagram), which evenly partition the space between neighbouring points, and uses partitions to construct cells for each point:

<p align="center">
<img src="figs/voronoi.png" alt="drawing" width="400"/>
</p>

By iteratively removing the points occupying the smallest cell areas, we are left with *n* points with maximum spread. When we apply this function to trait space using **20 species**, it looks like this:

<p align="center">
<img src="figs/figure1.png" alt="drawing" width="500"/>
</p>

> Which gives the following 20 species names: HIDDEN

The above species are selected for over three PC axes (i.e., in three dimensions), but displayed only on axes 1 and 2. The third principal component aligns strongly with colony size. Here is the select in three dimensions:

<p align="center">
<img src="figs/figure2.png" alt="drawing" width="500"/> </p>
<p align="center">

> Explore the 3D plot [here](https://mikemcwilliam.github.io/webGL/index.html).

At this point we have a list of 20 species that are most evenly spread in trait space, and so capture a broad range of trade-offs and thereby a higher chance of forming a functioning coral assemblage.

### Step 3: Weigh by qualities

The final step is to weight species selection by demonstrated qualities that are expected to help them persist. We still need to discuss how to do this, but to demonstrate the bet hedging framework we used the following criteria from the coral trait database:

- [GBR Abundance](https://coraltraits.org/traits/65) categories from Corals of the World (common=1; uncommon=0.25; rare=0.1).
- [Range size](https://coraltraits.org/traits/138) from Hughes et al. shapefiles (scaled as relative area between 0 and 1).
- [Genus fossil age](https://coraltraits.org/traits/116) from Paleobiology DB (scaled as relative age between 0 and 1).

The voronoi cell areas (from Step 2) are simply multiplied by each of these relative qualities. So, a species's cell area remains the same if it is common, large ranges and old-aged. When we do this, the voronoi function favours species with even spread in trait space and with higher levels of the relative qualities deemed important.

<p align="center">
<img src="figs/figure3.png" alt="drawing" width="500"/> </p>

> Which gives the following 20 species names: HIDDEN

We are also exploring *density* in PC space, which weighs species from clusters of species in trait space more (or less) heavily (scaled between 0 and 1). This needs discussion, but presumably species cluster evolutionarily in certain regions of trait space for a reason, and so perhaps one scenarios should look to reflect this.

<p align="center">
<img src="figs/figure4.png" alt="drawing" width="500"/> </p>

> Which gives the following 20 species names: HIDDEN

### Step 4: Do species represent potential winners, losers or both?

We had a quick look at this question using bleaching sensitivity index using data from [this paper](https://onlinelibrary.wiley.com/doi/abs/10.1111/gcb.13276). The selected species (red points, below) have a large range of bleaching sensitivities compared to the total distribution (histogram), but note that they do not include the most sensitive species:

<p align="center">
<img src="figs/BRI.png" alt="drawing" width="400"/> </p>


### Step 5: Can the selected species build a functioning reef?

This is a complex question that is difficult to address. However, we looked at the possibility of two approaches to explore the question of whether the selected species could support reef-building - arguably the most important coral function because most other functions rely on the presence of a consolidated reef framework. The two approaches are (i) by defining the three functional groups - builders, fillers, and cementers -described in [Goreau 1963](https://nyaspubs.onlinelibrary.wiley.com/doi/abs/10.1111/j.1749-6632.1963.tb13465.x), and (ii) comparing our species with the [seven common species](https://link.springer.com/article/10.1007/BF01771897) that have built Clipperton Atoll in remote the Eastern Pacific (note: I believe all the Clipperton species are also found on the Great Barrier Reef).

The somewhat arbitrary step is defining the traits of builders fillers and cementers. We could use a more rigorous approach, but for now we used:
- Builders: Large size (tall and wide), voluminous skeleton
- Fillers: Highly branching & large size
- Cementers: Large and flat

The is only a small amount of taxonomic alignment between the selected species and the Clipperton species, but the results show that the selected species occupy similar portions of trait space, and that they potentially represent each of the three functional groups:

<p align="center">
<img src="figs/figure5.png" alt="drawing" width="400"/> </p>


## Still to do

- Gather species-level abundance data for GBR species to weigh species selection
- Decide on how to generate index of 'desirability' to weigh selection
- Test whether selected species represent a large genetic diversity
- Restorability?
- Reproductive traits?
- Compare with *expert* species choice (the reason we haven't shown our results!)
