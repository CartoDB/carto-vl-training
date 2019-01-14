# CARTO VL training

Welcome to the CARTO VL training. This repository will support a training session covering several CARTO VL topics. It will lead you from the basics of creating a map to advanced techniques for developing powerful interactive visualizations. 

We recommend reviewing these slides first for a quick overview of how and why CARTO VL is useful for you: [http://bit.ly/carto-vl-training](http://bit.ly/carto-vl-training)


After completing these training modules, you will be able to create your first CARTO VL map. We also link to the [CARTO VL documentation](https://carto.com/developers/carto-vl/) and [guides](https://carto.com/developers/carto-vl/guides/introduction/) throughout, so you have resources for further information. After you go through the training, please send us your feedback about the session so we can improve the documentation and guides.

## What is CARTO VL?

[CARTO VL](https://github.com/cartodb/carto-vl) is a JavaScript library used to create custom location intelligence applications that leverage the power of [CARTO](https://carto.com/). It uses [WebGL](https://www.khronos.org/webgl/) to enable powerful vector maps.

It relies on [Mapbox GL](https://www.mapbox.com/mapbox-gl-js/api) to render the basemaps. Mapbox GL can be used for other functionality too, read the [Mapbox GL documentation](https://www.mapbox.com/mapbox-gl-js/api/) for more information. However, keep in mind that CARTO VL layers can only be controlled with the CARTO VL API and that Mapbox GL native layers can **only** be controlled with the Mapbox GL API. Therefore, CARTO VL expressions cannot be used for Mapbox GL layers and vice versa.

# Requirements

 - [Git](https://services.github.com/on-demand/github-cli/git-configuration) and [this repository, cloned](https://services.github.com/on-demand/github-cli/clone-repo-cli).
 - Basic knowledge of HTML, CSS and JavaScript would be helpful.
 - A text editor and an Internet connection.

# Sections

 1. [Getting Started](01-getting-started.md)
 2. [Using Data in Your Visualization with Sources](02-using-sources.md)
 3. [Styling Properties Using Expressions](03-style-with-expressions.md)
 4. [Introduction to Ramps and Data-Driven Visualizations](04-data-driven-styles.md)
 5. [Using Legends](05-legends.md)
 6. [Aggregation](06-cluster.md)
 7. [Zoom-Based Styles](07-zoom-based-styles.md)
 8. [Animation](08-animation.md)
 9. [Intro to Interactivity and Events](09-interactivity.md)

## How to use this repository

Attending and following a training session should not be a stressful experience. This repository is split into multiple sections. Each of the sections will have several steps. You can easily jump between the sections and steps as needed, since each of them has a title and a link.