### Prerequisites:
* A computer with a code editor
  * Notepad (Windows default)
  * TextEdit (Mac default)
  * [Sublime Text](https://www.sublimetext.com/)
  * [Atom](https://atom.io/)
___

## Getting Started
*Take the next steps to set up a basic CARTO VL map & view it in your browser.*
*For more help check out our Developer Center's Getting Started documentation [here](https://carto.com/developers/carto-vl/guides/getting-started/).*

### Create a Basic Map
1. Open a new document in your code editor, then paste this into it:

    ```html
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
          style: carto.basemaps.voyager,
          center: [-3.6908, 40.4297],
          zoom: 11
        });
      </script>
    </body>

    </html>
    ```
  
    **WHY MAPBOX GL?**
    * Notice we are including Mapbox GL JavaScript and style libraries. 
    * CARTO VL uses [Mapbox GL](https://www.mapbox.com/mapbox-gl-js/api/) to render basemaps. 
    * We will use CARTO VL code to add CARTO data layers over the basemap, but because the Mapbox GL libraries are included you also have the option to add native Mapbox data layers to your map.
    * CARTO VL expressions cannot be used for native Mapbox GL layers and vice versa.
    
    **THE MAP OBJECT**
    * `const map = new mapboxgl.Map` gives us a map object. This will contain our visualization.
    * `container: 'map',` puts our map object in this HTML element: `<div id="map"></div>`. 
      * The HTML element acts as a container.
      * We want the map to fill the whole web page in our browser. To do that we define styles for the map's container, inside the `<style>` element.
    * `style: carto.basemaps.voyager` defines which basemap to use. You also have two other basemaps to choose from:
      * `carto.basemaps.positron`
      * `carto.basemaps.darkmatter`
    * `center: [0, 0]` will center your map on these coordinates.
    * `zoom: 0` displays the map at this default zoom level when it loads.
    * `scrollZoom: false`: by default you can zoom your map with your trackpad or mouse's scroll wheel. Add this parameter and set it to `false` to disable that. 
      * We won't need it since we are adding zoom control buttons with `new mapboxgl.NavigationControl`
    
2. Save this file as `index.html` on your computer.
3. Open index.html in your web browser.
    
    *Now you should see this:*
   
    ![screen shot 2018-10-30 at 4 14 34 pm](https://user-images.githubusercontent.com/1779444/47747540-ef9ed300-dc5e-11e8-9b2c-66a0c012519b.png)
    
### Add Credentials
*To add other layers on top of the basemap we need access to CARTO datasets. In this example we will use [public](https://carto.com/help/building-maps/privacy-settings-for-protecting-maps-and-data/) data from a CARTO account.*

*Because data privacy is important at CARTO, authentication is required. We use api keys for that. Find out more about how CARTO authentication works [here](https://carto.com/developers/fundamentals/authorization/).*

4. Add this code block beneath `map.addControl(nav, 'top-left');`

    ```html
    carto.setDefaultAuth({
      username: 'cartovl',
      apiKey: 'default_public'
    });
    ```
    
    * `username` is the name of the CARTO account that contains our data.
    * The `default_public` key gives a CARTO VL app access to all of an account's public datasets.
    * You can add a code block like this to your app more than once, so you can pull data from more than one CARTO account into the same map.