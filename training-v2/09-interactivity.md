## Intro to Interactivity and Events

One of the most useful features of CARTO maps is that they're interactive. When users click on a map, or pan it, or hover over it's features, we can cause another action to happen in the map. For example, we can open a Pop-Up window, or change the color of a feature to highlight it. In this section we will cover different types of interactivity and how you can use them to highlight your data. We also have a guide for this [here](https://carto.com/developers/carto-vl/guides/add-interactivity-and-events/).

### Create a Basic Map

Let's create a new map using world population data.

1. Paste this into your index.html document:

    ```
    <!DOCTYPE html>
    <html>

    <head>
        <title>CARTO VL training</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta charset="UTF-8">
        <!-- Mapbox GL -->
        <link href="https://api.tiles.mapbox.com/mapbox-gl-js/v0.50.0-beta.1/mapbox-gl.css" rel="stylesheet" />
        <script src="https://api.tiles.mapbox.com/mapbox-gl-js/v0.50.0-beta.1/mapbox-gl.js"></script>
        <!-- CARTO VL JS -->
        <script src="https://libs.cartocdn.com/carto-vl/v0.9.1/carto-vl.min.js"></script>
        <link href="https://carto.com/developers/carto-vl/examples/maps/style.css" rel="stylesheet">
    </head>

    <body>
        <div id="map"></div>
        <script>
            const map = new mapboxgl.Map({
                container: 'map',
                style: carto.basemaps.voyager,
                center: [0, 40],
                zoom: 1
            });

            carto.setDefaultAuth({
                user: 'cartovl',
                apiKey: 'default_public'
            });

            const source = new carto.source.Dataset('populated_places');
            const viz = new carto.Viz(`
                color: grey
                width: 6
            `);
            const layer = new carto.Layer('layer', source, viz);

            layer.addTo(map);
        </script>
    </body>

    </html>
    ```

The first step to making something happen when a user interacts with the map is detecting that user's action. In the following sections we will show you the ways CARTO VL "listens" for these events.

### Listen for Map Events

2. Add this under `<div id="map"></div>` to add an overlay box. We are setting this up to show basic information about our map, in the paragraph element with `desc` id.

    ```
    <aside class="toolbox">
        <div class="box">
            <header>
                <h1>Events</h1>
            </header>
            <section>
                <p id="desc"></p>
            </section>
        </div>
    </aside>
    ```

    Next we will set up some variables to hold the basic information about our map.

3. Paste this under your `const layer = new carto.Layer('layer', source, viz);` line:

    ```
    function desc() {
        const center = map.getCenter();
        const longitude = center.lng.toFixed(6);
        const latitude = center.lat.toFixed(6);
        const bearing = map.getBearing().toFixed(0);
        const zoom = map.getZoom().toFixed(2);
        document.querySelector('#desc').innerHTML = `Center: [${longitude}, ${latitude}]<br/>Zoom: ${zoom}<br/>Bearing: ${bearing}º`;
    }
    ```

    The functions we're using to define these variables come from Mapbox GL. We can use them since our CARTO VL map is based on a Mapbox GL map object.
    * `center` will contain the coordinates of the map's center point, based on it's bounding box.
        * [getCenter](https://www.mapbox.com/mapbox-gl-js/api/#lnglatbounds#getcenter)
    * `longitude` will contain the `center` longitude.
    * `latitude` will contain the `center` latitude.
    * `bearing` will contain the current compass "up" direction, in degreees. 0 means "up" is North.
        * [getBearing](https://www.mapbox.com/mapbox-gl-js/api/#map#getbearing)
    * `zoom` will contain the map's current zoom level.
        * [getZoom](https://www.mapbox.com/mapbox-gl-js/api/#map#getzoom)
    * The last line displays the information from our variables in the overlay box we created in the last step.

    Now we just need to run the `desc` function, to detect the information we will display in our overlay. 

4. Add these lines beneath the code block you added in the last step:

    ```
    map.on('load', desc);
    map.on('move', desc);
    ```

    * We already defined `map` as the name of our map object. 
    * [load](https://www.mapbox.com/mapbox-gl-js/api/#map.event:load) is a Mapbox GL function that will detect when the map loads in a browser.
    * [move](https://www.mapbox.com/mapbox-gl-js/api/#map.event:move) is a Mapbox GL function that will detect when a map user moves the map, for example by panning.

    When you save these changes and open index.html in a web browser your map should look like this. Notice how the overlay values change as we pan the map.

    ![map-events](images/training-v2-09-map-events.gif)



