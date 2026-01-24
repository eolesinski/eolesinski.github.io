---
layout: page
title: PoliSciPy
description: A Python Library for Political Data Analysis & U.S. Election Visualization
img: assets/img/election_2024.png
importance: 1
category: code & open-source
related_publications: false
---

## PoliSciPy
### A Python Library for U.S. Election Visualization

[PoliSciPy](https://poliscipy.github.io/poliscipy/) is an open-source Python package that simplifies the creation of U.S. electoral college maps and political data analysis. What typically requires hundreds of lines of code with GeoPandas and matplotlib can be accomplished with a single function call.

[GitHub Repository](https://github.com/poliscipy/poliscipy) | [Documentation](https://poliscipy.github.io/poliscipy/) | [PyPI](https://pypi.org/project/poliscipy/) | [Conda](https://anaconda.org/channels/conda-forge/packages/poliscipy/overview)

---

### Overview
Creating high-quality electoral maps in Python traditionally involves multiple complex steps: loading shapefiles, repositioning Alaska and Hawaii, adding state labels, applying custom colormaps, and formatting the visualization. PoliSciPy handles all of this automatically, allowing researchers and analysts to focus on their data rather than cartographic details.

### Key Features

- **Single-line map generation:** Create complete electoral maps by passing a single data column
- **Partisan colormap:** Use custom color schemes for representing political leanings and competitiveness
- **Visually appealing geography:** Properly positioned Alaska and Hawaii with centered state labels
- **Flexible analysis:** Built for making highly customizable election maps for election data analysis and research
- **Publication-ready output:** Quickly create high-quality visualizations suitable for reports and presentations

---

### How It Works
PoliSciPy improves upon existing political science data visualization workflows by incorporating custom-edited shapefiles, streamlined geometric transformations, and allowing a high degree of customization. The technical approach to the project involved three main steps:

1. Shapefile Preprocessing
Using [ArcGIS](https://www.arcgis.com/index.html) I edited U.S. Census Bureau shapefiles to move state polygons and add a `x_centroid` and `y_centroid` column to each state. This allows for state labels to be automatically positioned at the visual center of each state, eliminating the need for manual coordinate adjustments.

2. Geometric Transformations
Alaska and Hawaii are repositioned and scaled for better visibility on the continental map. The transformations are applied to each polygon's coordinates using lambda functions to ensure the entire multipolygon shape is properly adjusted.

3. Custom Colormap Integration
PoliSciPy includes a partisan colormap designed specifically for electoral data, making it easy to represent political leaning or competitiveness across states without manually defining color schemes.

**With PoliSciPy**

```python
# Plot the electoral college map for the year 2024
plot_electoral_map(gdf, column='winning_party', title='2024 U.S. Electoral College Map')
```

### Example Output

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/election_2024.png" title="example image" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    Electoral college map (2024) created using the PoliSciPy package.
</div>

You can also create election maps at a county-level granularity:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/county-2024.png" title="example image" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    County level election results (2024) created using the PoliSciPy package.
</div>



<!-- 

We then perform the following geometric transformations to the state polygons for Alaska and Hawaii after moving them to a more easily visible location:

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3 mt-md-0">
    \[
    Hawaii = \begin{bmatrix}
    x' \\
    y' 
    \end{bmatrix} = \begin{bmatrix}
    1.1 & 0 \\
    0 & 1.0 
    \end{bmatrix} * \begin{bmatrix}
    x \\
    y 
    \end{bmatrix}
    \]
  </div>
  <div class="col-sm-6 mt-3 mt-md-0">
    \[
    Alaska = \begin{bmatrix}
    x' \\
    y' 
    \end{bmatrix} = \begin{bmatrix}
    0.62 & 0 \\
    0 & 1.0 
    \end{bmatrix} * \begin{bmatrix}
    x \\
    y 
    \end{bmatrix}
    \]
  </div>
</div>

The figure below shows a Jupyter notebook illustrating how a geometric transformation is applied to a state's multipolygon once it has been edited in ArcGIS. To make sure that the transformation is applied to the entire shape, a lambda function is used to apply the scale factor to each of the polygon's coordinates.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/alaska.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
    </div>
</div>
<div class="caption">
    The application of a geometric transformation to a multipolygon in a Jupyter Notebook.
</div>

Once the geometric transformations are applied, the only thing left to do is add the labels for each of the states. Editing the shapefile in ArcGIS allowed for the addition of a `x_centroid` and `y_centroid` column directly to the shapefile so that each state label could be displayed in the center of its respective multipolygon.

<div class="row">
  <div class="col-md-7">
    <p>PoliSciPy also includes a custom colormap for displaying commonly used electoral map colors.
    This partisan color scheme can be used to represent the political leaning or relative competitiveness of
    a particular state.</p>
  </div>
  <div class="col-md-5">
    {% include figure.liquid path="assets/img/colormap_2.png" title="example image" class="img-fluid" %}
  </div>
</div>

Without using the PoliSciPy package, creating an electoral college map using GeoPandas and matplotlib would require multiple steps. These steps would include, <em>inter alia</em>, creating the plot, moving the states, adding labels, creating a custom color map, and displaying a total results bar.

An example of some of the code that would be required:

{% raw %}

```python
# Create a figure and axis
fig, ax = plt.subplots(figsize=(20, 10))

# Create a custom colormap for red, blue, and light gray
colors = ['#4875b1','lightgray','#b82b2b']
cmap = ListedColormap(colors)

# Plot the choropleth map
gdf_election_c.plot(column='winning_party', cmap=cmap, categorical=True, legend=True,
                    ax=ax, edgecolor='white', linewidth=.5)
```

{% endraw %}

Using the PoliSciPy package makes this entire process simpler by only requiring a single function call to generate a full electoral college map of the United States. The user only needs to pass through one parameter - a column containing the election results - to generate the plot.

An example of an electoral college map created using the PoliSciPy package is shown below:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/election_2024.png" title="example image" class="img-fluid" %}
    </div>
</div>
<div class="caption">
    Electoral college map (2024) created using the PoliSciPy package.
</div>

-->

