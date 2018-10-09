# CARTO VL training

Welcome to the CARTO VL training. This repository will support a training session covering several topics around CARTO VL. The existing [CARTO VL documentation](https://carto.com/developers/carto-vl/) is a useful resource, however, this training is derived from the future version of the CARTO VL documentation and guides. It will lead you from the basics of creating a map to advanced techniques for developing powerful interactive visualizations. After reading this guide, you will be able to create your first CARTO VL map. After you go through the training, send any feedback about the session so we can improve the new documentation and guides.

## What is CARTO VL?

[CARTO VL](https://github.com/cartodb/carto-vl) is a JavaScript library to create custom location intelligence applications that leverage the power of [CARTO](https://carto.com/). It uses [WebGL](https://www.khronos.org/webgl/) to enable powerful vector maps.

It relies on [Mapbox GL](https://www.mapbox.com/mapbox-gl-js/api) to render the basemaps. Mapbox GL can be used for other functionality too, read [Mapbox GL documentation](https://www.mapbox.com/mapbox-gl-js/api/) for more information. However, keep in mind that CARTO VL layers can only be controlled with the CARTO VL API and that Mapbox GL native layers can **only** be controlled with the Mapbox GL API. Therefore, CARTO VL expressions cannot be used for Mapbox GL layers and vice versa.

# Requirements

 - [Git](https://services.github.com/on-demand/github-cli/git-configuration) and [this repository cloned](https://services.github.com/on-demand/github-cli/clone-repo-cli).
 - Basic knowledge of HTML, CSS and JavaScript would be helpful.
 - A text editor and an Internet connection.

# Sections

 1. Getting started with CARTO VL.
 1. Using data in your visualization with Sources.
 1. Styling properties using expressions.
 1. Data Driven Visualization.
 1. Widgets and Legends.
 1. Aggregating Data.
 1. Using multiscale properties.
 1. Playing with animations.
 1. Interactivity and Events.

## How to use this repository

Attending and following a training session should not be an stressful experience, this repository allows to jump to specific points in time. You can move between the different sections, and to be more specific, each of the sections will have several steps. You only need to checkout the tag that matches the section and step.

#### Jump to the first step in the Getting started section
```shell
git checkout section-1-step-1
```

#### List all sections and steps
```shell
git tag
```
