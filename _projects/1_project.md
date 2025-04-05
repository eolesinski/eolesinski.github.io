---
layout: page
title: PoliSciPy
description: A Python Library for Political Data Analysis & U.S. Election Visualization
img: assets/img/election_2024.png
importance: 1
category: code & open-source
related_publications: false
---

PoliSciPy is an open-source Python package for psephologists. It makes it easy to perform a wide range of analysis using election data. For example, you can easily construct high-quality electoral college maps by simply passing in a single data column.

This Python package improves upon the geoStates package by adding additional features and rewriting its core functional logic. The key to simplifying the code required for generating these maps involves using the [ArcGIS](https://www.arcgis.com/index.html) geospatial data software to edit shapefiles provided by the U.S. Census Bureau.

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
