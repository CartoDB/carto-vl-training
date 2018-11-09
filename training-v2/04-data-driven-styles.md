## Introduction to Ramps and Data-Driven Visualizations



### Create a Basic Map
1. For this section let's start with a map of UK elections. Leave the `viz` object empty for this step:

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
                center: [-3, 54.8],
                zoom: 4.5
            });

            carto.setDefaultAuth({
                user: 'cartovl',
                apiKey: 'default_public'
            });

            const source = new carto.source.Dataset('uk_elections');
            const viz = new carto.Viz();
            const layer = new carto.Layer('layer', source, viz);

            layer.addTo(map);
        </script>
    </body>

    </html>
    ```


### Ramp and Numeric Properties

    ```
    const source = new carto.source.Dataset('pop_density_points');

    const viz = new carto.Viz(`
      width: 2
      color: ramp($dn, [black, yellow])
      strokeWidth: 0
    `);
    ```

### Improve the Style

    ```
    const viz = new carto.Viz(`
      width: 2
      color: ramp($dn, [green, yellow, red])
      strokeWidth: 0
    `);
    ```

### Classify a Numeric Property for Better Perception

    ```
    const viz = new carto.Viz(`
      width: 1.5
      color: ramp(globalQuantiles($dn, 3), [green, yellow, red])
      strokeWidth: 0
    `);
    ```

### The `Others` Category

    ```
    const source = new carto.source.Dataset('uk_elections');
    
    const viz = new carto.Viz(`
      color: ramp(buckets($winner, ["Conservative Party", "Labour Party"]), [blue, red], white)
      strokeColor: opacity(white, 0.6)
    `);
    ```

### Find the Most Common Categories

    ```
    const source = new carto.source.Dataset('dot_rail_safety_data');
    
    const viz = new carto.Viz(`
      width: 10
      strokeWidth: 0.2
      color: ramp(top($accident_type, 3), [#3969AC, #F2B701, #E73F74], #A5AA99)
    `);
    ```

### Showing All Categories for Exploratory Analysis

    ```
    const viz = new carto.Viz(`
      width: 10
      strokeWidth: 0.2
      color: ramp($accident_type, [#7F3C8D,
      #11A579,
      #3969AC,
      #F2B701,
      #E73F74,
      #80BA5A])
    `);
    ```

### CARTOColors

    ```
    const source = new carto.source.Dataset('pop_density_points');
    
    const viz = new carto.Viz(`
      width: 2
      color: ramp($dn, temps)
      strokeWidth: 0
    `);
    ```

### Create a Bubble Map

    ```
    const source = new carto.source.Dataset('dot_rail_safety_data');
    
    const viz = new carto.Viz(`
      width: ramp($total_damage, [0, 50])
      strokeWidth: 0.2
      color: ramp(top($accident_type, 3), [#3969AC, #F2B701, #E73F74], #A5AA99)
    `);
    ```

### Size Perception

    ```
    const viz = new carto.Viz(`
      width: sqrt(ramp($total_damage, [0, 50^2]))
      strokeWidth: 0.2
      color: ramp(top($accident_type, 3), [#3969AC, #F2B701, #E73F74], #A5AA99)
    `);
    ```

### Introducing Symbols and Images

    ```
    const viz = new carto.Viz(`
      width: sqrt(ramp($total_damage, [0, 50^2]))
      strokeWidth: 0.2
      color: ramp(top($accident_type, 3), [#3969AC, #F2B701, #E73F74], #A5AA99)
      symbol: ramp(top($accident_type, 3), [star, triangle, square])
    `);
    ```


