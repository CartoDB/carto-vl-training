# CARTO VL training

Welcome to the CARTO VL training. This repository will support a training session covering several CARTO VL topics. It will lead you from the basics of creating a map to advanced techniques for developing powerful interactive visualizations. After reading this guide, you will be able to create your first CARTO VL map. We also link to the [CARTO VL documentation](https://carto.com/developers/carto-vl/) and [guides](https://carto.com/developers/carto-vl/guides/introduction/) throughout, so you have resources for further information. After you go through the training, please send us your feedback about the session so we can improve the documentation and guides.

## What is CARTO VL?

[CARTO VL](https://github.com/cartodb/carto-vl) is a JavaScript library used to create custom location intelligence applications that leverage the power of [CARTO](https://carto.com/). It uses [WebGL](https://www.khronos.org/webgl/) to enable powerful vector maps.

It relies on [Mapbox GL](https://www.mapbox.com/mapbox-gl-js/api) to render the basemaps. Mapbox GL can be used for other functionality too, read the [Mapbox GL documentation](https://www.mapbox.com/mapbox-gl-js/api/) for more information. However, keep in mind that CARTO VL layers can only be controlled with the CARTO VL API and that Mapbox GL native layers can **only** be controlled with the Mapbox GL API. Therefore, CARTO VL expressions cannot be used for Mapbox GL layers and vice versa.

# Requirements

 - [Git](https://services.github.com/on-demand/github-cli/git-configuration) and [this repository, cloned](https://services.github.com/on-demand/github-cli/clone-repo-cli).
 - Basic knowledge of HTML, CSS and JavaScript would be helpful.
 - A text editor and an Internet connection.

# Sections

 1. Getting Started
 2. Using Data in Your Visualization with Sources
 3. Styling Properties Using Expressions
 4. Introduction to Ramps and Data-Driven Visualizations
 5. Using Legends
 6. Aggregation
 7. Zoom-Based Styles
 8. Animation
 9. Intro to Interactivity and Events

## How to use this repository

Attending and following a training session should not be a stressful experience. This repository is split into multiple sections. Each of the sections will have several steps. You can easily jump between the sections and steps as needed, since each of them has a title and a link.