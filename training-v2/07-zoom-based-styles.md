## Zoom-Based Styles

In the last section we sized points proportionally according to total velocity / number of points being aggregated. This looks fine at our default zoom level, but look what happens when we zoom in:

![no-zoom-styles](images/training-v2-07-no-zoom-styles.gif)

We can make the points much easier to see at different zoom levels when we use CARTO VL's [scaled](https://carto.com/developers/carto-vl/reference/#cartoexpressionsscaled) expression. See more detail about it [in this guide](https://carto.com/developers/carto-vl/guides/zoom-based-styles/).

### Create a Basic Map

Let's continue with our Central Park map from the last section.

1. Let's create a new basic map:

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

        <aside class="toolbox">
            <div class="box">
                <header>
                    <h1>Rendered features</h1>
                </header>
                <section>
                    <div id="controls">
                        <div id="content"></div>
                        <ul id="content-legend"></ul>
                    </div>
                </section>
                <footer class="js-footer"></footer>
            </div>
        </aside>

        <script>
            const map = new mapboxgl.Map({
                container: 'map',
                style: carto.basemaps.darkmatter,
                center: [-73.9684, 40.7828],
                zoom: 13
            });

            carto.setDefaultAuth({
                user: 'cartovl',
                apiKey: 'default_public'
            });

            const source = new carto.source.Dataset('million_walks_central_park');
            const viz = new carto.Viz(`
                width: ramp(clusterSum($velocity)/clusterCount(), [0, 0.5])
                color: ramp(clusterMode($travel_mode), bold)
                strokeWidth: 0
                resolution: 0.25
            `);
            const layer = new carto.Layer('layer', source, viz);

            layer.addTo(map);
            layer.on('loaded', updateRenderedFeatured);
            layer.on('updated', updateRenderedFeatured);

            function updateRenderedFeatured() {
                document.querySelector('#content').innerText = layer.getNumFeatures().toLocaleString();
            }

            layer.on('loaded', () => {
                const colorLegend = layer.viz.color.getLegendData();
                let colorLegendList = '';
                 function rgbToHex(color) {
                    return "#" + ((1 << 24) + (color.r << 16) + (color.g << 8) + color.b).toString(16).slice(1);
                }
                colorLegend.data.forEach((legend, index) => {
                    const color = legend.value
                        ? rgbToHex(legend.value)
                        : 'white'
                     if (color) {
                        colorLegendList +=
                            `<li><span class="point-mark" style="background-color:${color}; border: 1px solid black;"></span><span>${legend.key.replace('CARTO_VL_OTHERS', 'Other causes')}</span></li>\n`;
                    }
                });
                 document.getElementById('content-legend').innerHTML = colorLegendList;
            });
        </script>
    </body>

    </html>
    ```

### Scale the Symbol Size

2. Wrap your width expression in a `scaled` function, like this:

    `width: scaled(ramp(clusterSum($velocity)/clusterCount(), [0, 0.5]), 13)`

    * `Scaled` takes a width expression as it's first parameter.
    * It's second parameter is a zoom level: 13.
      * You should choose the zoom level at which your map looks best with the current styles.
      * CARTO VL will automatically base the other zoom level styles on zoom 13, just scaled so they are sized appropriately for the current zoom. 

    Now check out how the map appears when we zoom in:

    ![scaled-styles](images/training-v2-07-zoom-styles.gif)