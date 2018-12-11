# Using Data in Your Visualization with Sources

*Sources are the basis for your map. They provide the data that you will visualize. In this section we'll demonstrate a few different ways to use them.*

*For more information check our [Add Data Sources guide](https://carto.com/developers/carto-vl/guides/add-data-sources/).*

## Create a Basic HTML Template

Let's start with the map we made in the Getting Started section. Open it in your code editor.

```html
<!DOCTYPE html>
<html>

<head>
  <title>CARTO VL Training</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta charset="UTF-8">
  <!-- Include CARTO VL JS from the CARTO CDN-->
  <script src="https://libs.cartocdn.com/carto-vl/v1.0.0/carto-vl.min.js"></script>
  <!-- Include Mapbox GL from the Mapbox CDN-->
  <script src="https://api.tiles.mapbox.com/mapbox-gl-js/v0.50.0/mapbox-gl.js"></script>
  <link href="https://api.tiles.mapbox.com/mapbox-gl-js/v0.50.0/mapbox-gl.css" rel="stylesheet" />
  <!-- Include CARTO styles-->
  <link href="https://carto.com/developers/carto-vl/examples/maps/style.css" rel="stylesheet">
  <style>
    body {
      margin: 0;
      padding: 0;
    }

    #map {
      position: absolute;
      width: 100%;
      height: 100%;
    }
  </style>
</head>

<body>
  <div id="map"></div>

  <script>
    const map = new mapboxgl.Map({
      container: 'map',
      style: carto.basemaps.voyager,
      center: [-3.6908, 40.4297],
      zoom: 11
    });

    carto.setDefaultAuth({
      user: 'cartovl',
      apiKey: 'default_public'
    });

    const source = new carto.source.Dataset('madrid_listings');
    const viz = new carto.Viz(`
      color: green
      width: 20
    `);
    const layer = new carto.Layer('layer', source, viz);

    layer.addTo(map);
  </script>
</body>

</html>
```

## Dataset Source with Custom Credentials

One powerful feature of CARTO VL is that you can use data from a few different sources in the same map. Replace the existing `source` with a dataset from a different CARTO account:

```javascript
const citiesSource = new carto.source.Dataset('populated_places', {
  username: 'documentation',
  apiKey: 'default_public'
});
```

* Notice we're still using the Dataset source, but this time we're using an optional second parameter.
* We have already defined default authorization in the `setDefaultAuth` function, but this second parameter authorizes this map to use the `populated_places` dataset from a different CARTO account.
* The Dataset source actually accepts three parameters, find out more [here](https://carto.com/developers/carto-vl/reference/#cartosourcedataset).

Make sure to update the layer definition with the new source name:

```javascript
const layer = new carto.Layer('layer', citiesSource, viz);`
```

## Add a GeoJSON Source and Layer

CARTO VL also provides other ways to pull in source data. For example you can use a [SQL source](https://carto.com/developers/carto-vl/reference/#cartosourcesql) like this:

```javascript
const citiesSource = new carto.source.SQL('SELECT * FROM populated_places WHERE pop_max > 1000000', {
  username: 'documentation',
  apiKey: 'default_public'
});
```

This is useful if:

* you only want to use part of a dataset.
* you want to manipulate the original data with [PostgreSQL](https://carto.com/help/working-with-data/easy-sql/) or [PostGIS](https://carto.com/help/diy/postgis/) and use the results in your map.

Our `citiesSource` query is letting us use only large cities from the `populated_places` dataset. That's happening because our query contains a WHERE clause that will only select cities with a maximum population of more than one million people. See which kinds of sources you can use and example code [here](https://carto.com/developers/carto-vl/reference/#cartosource) in our documentation.

In this map let's add a second layer that uses a GeoJSON source. We want this layer to show CARTO's Madrid office location. Add this to your code:

```javascript
const office = {
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [-3.70379, 40.416775]
      },
      "properties": {
        "address": "Madrid, Spain"
      }
    }
  ]
};
```

We've put the GeoJSON into a `const` variable. Now we can use it as a source when we add code like this:

```javascript
const officeSource = new carto.source.GeoJSON(office);
```

Now add styles for the GeoJSON source and create a layer with them. Add the layer to your map object.

```javascript
const officeViz = new carto.Viz(`
  color: red
  width: 50
`);

const officeLayer = new carto.Layer('office', officeSource, officeViz);

officeLayer.addTo(map);
```

*When you save these changes and open your code document in a browser, your map should show a green point for the city of Madrid, and a red point for the CARTO office, like this:*

![two-sources](images/training-v2-02-srcs.png)
