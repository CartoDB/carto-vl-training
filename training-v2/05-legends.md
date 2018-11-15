## Using Legends

There's one thing missing from our maps so far: Legends. Every good map should use a legend that explains it's features at a glance.

### Create a Basic Map
1. Let's continue with our map from the last section:

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
              style: carto.basemaps.darkmatter,
              center: [-96, 41],
              zoom: 3
            });

            carto.setDefaultAuth({
                user: 'cartovl',
                apiKey: 'default_public'
            });

            const source = new carto.source.Dataset('dot_rail_safety_data');
            const viz = new carto.Viz(`
              width: sqrt(ramp($total_damage, [0, 50^2]))
              strokeWidth: 0.2
              color: ramp(top($accident_type, 3), [#3969AC, #F2B701, #E73F74], #A5AA99)
              symbol: ramp(top($accident_type, 3), [star, triangle, square])
            `);
            const layer = new carto.Layer('layer', source, viz);

            layer.addTo(map);
        </script>
    </body>

    </html>
    ```

    ![image-icons](images/training-v2-04-image-icons.png)

### Add a Legend

2. Add an HTML element that will contain our Legend, by pasting this into your code under `<div id="map"></div>`:

    ```
    <aside class="toolbox">
        <div class="box">
            <header>
                <h1>Type of accident</h1>
            </header>
            <section>
                <div id="controls">
                    <ul id="content"></ul>
                </div>
            </section>
            <footer class="js-footer"></footer>
        </div>
    </aside>
    ```

    When you save this and open your HTML file in a browser, it should look like this:

    ![legend-container](images/training-v2-05-legend-container.png)

    Notice there's not much content related to the actual map features yet. At this point we're just setting up a container.
    * [`aside`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/aside) is an HTML element used as a container for content that's considered separate from the page's main content.
    * We're also using a CARTO-specific `box` class to define styles for the Legend container...basically making it a white box with round edges.
    * The [`header` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) is where we're storing our Legend title. 
      * We're using default [`h1`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements) tags to define the font style for our title.
      * You can modify this to use other [section heading elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements) or text styles as needed.
    * [`section`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) is an HTML element that's used to group content. 
    * Find out more about the footer element [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer).

One of the great things about CARTO VL is that it provides a function to auto-detect our map layer's data and styles: [`getLegendData()`](https://carto.com/developers/carto-vl/reference/#expressionsrampgetlegenddata). We can use that to create our Legend elements.

3. Paste this under `layer.addTo(map);`:

    ```
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
      document.getElementById('content').innerHTML = colorLegendList;
    });
    ```

    Now our legend contains icons representing our map features, and a label to let our viewers identify what they represent.

    ![legend-content](images/training-v2-05-legend-content.png)

    * After the map layer's feature colors are retrieved using `getLegendData`, `rgbToHex()` converts them to [hexadecimal notation](https://developer.mozilla.org/en-US/docs/Web/HTML/Applying_color#RGB_values).
    * The next function creates a Legend item containing a color icon and a label. It uses the information retrieved by `getLegendData` to generate the proper color and label for each type of map feature.



