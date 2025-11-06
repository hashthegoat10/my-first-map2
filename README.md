<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>My First Map With Markers</title>
  <meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
  <link href="https://api.mapbox.com/mapbox-gl-js/v3.15.0/mapbox-gl.css" rel="stylesheet">
  <script src="https://api.mapbox.com/mapbox-gl-js/v3.15.0/mapbox-gl.js"></script>
  <style>
    body {
      margin: 0;
      padding: 0;
    }

    img {
      width: 200px;
    }

    #map {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 100%;
    }
  </style>
</head>

<body>
  <div id="map"></div>
  <script>
    mapboxgl.accessToken = 'pk.eyJ1IjoiZG9tbGV0IiwiYSI6ImNtZzVyeG1hYTA3cXEyaXE0Ymp6MHBsNDIifQ.PBPONoWC4rGjYQCPHtF-bw';
    const map = new mapboxgl.Map({
      container: 'map',
      /*
      Choose from Mapbox's core styles, or make your own style with Mapbox Studio
      Mapbox Outdoors: mapbox://styles/mapbox/outdoors-v12
      Mapbox Light: mapbox://styles/mapbox/light-v11
      Mapbox Dark: mapbox://styles/mapbox/dark-v11
      Mapbox Satellite: mapbox://styles/mapbox/satellite-v9
      Mapbox Satellite Streets: mapbox://styles/mapbox/satellite-streets-v12
      Mapbox Streets: mapbox://styles/mapbox/streets-v12
      */
      style: 'mapbox://styles/hashthegoat10/cmhl6dq9q00hq01rg0uf6atz9',
      center: [-122.13951974752811, 37.731865103479485],
      zoom: 7
  
    
    });

    map.on('load', () => {
      map.addSource('my-places', {
        'type': 'geojson',
        'data': {
          'type': 'FeatureCollection',
          'features': [
            {
              'type': 'Feature',
              'geometry': {
                'type': 'Point',
                'coordinates': [-122.27734199157183, 37.78392195061235]
              },
              "properties": {
                'name': " In N Out",
                'description': "my favorite fast food",
                'image': "img/inout.webp",
                
              }
            },
            {
              'type': 'Feature',
              'geometry': {
                'type': 'Point',
                'coordinates': [-121.89741200393749, 37.41589987762532]
              },
              "properties": {
                'name': "Great Mall",
                'description': "i like shopping here",
                'image': "img/greatmall.jpg",
              }
            },
            {
              'type': 'Feature',
              'geometry': {
                'type': 'Point',
                'coordinates': [ -122.20320449880029, 37.7508559018307]
              },
              "properties": {
                'name': "Oakland Arena",
                'description': "i went to my first concert here",
                'image': "img/arena.webp",
              }
            }
          ]
        }
      });
      map.addLayer({
        'id': 'my-places',
        'type': 'circle',
        'source': 'my-places',
        'paint': {
          'circle-radius': 6,
          'circle-color': '#B42222'
        },
        'filter': ['==', '$type', 'Point']
      });

      // add popup on click
      map.addInteraction('popup', {
        type: 'click',
        target: { layerId: 'my-places' },
        handler: (e) => {
          const coordinates = e.feature.geometry.coordinates.slice();
          const name = e.feature.properties.name;
          const description = e.feature.properties.description;
          const image = e.feature.properties.image;

          new mapboxgl.Popup()
            .setLngLat(coordinates)
            .setHTML("<strong>" + name + "</strong><br/>" + description)
            .setHTML("<img src='" + image + "'><br><strong>" + name + "</strong><br/>" + description)
            .addTo(map);
        }
      });
    });

  </script>

</body>

</html>
# My Favorite Places 

!["Bike The Bay" App](img/header.png)

## What did I build?

["Bike The Bay" App](https://domlet.github.io/postsession25)  is a one-page, mobile-friendly web app that offers interactive maps for five cycling routes in the SF Bay Area. 

Users can...
1. **Toggle through all the maps**, by tapping the `1` `2` `3` `4` `5` numbers at the bottom of the screen. 
1. **Explore each map** by using gestures to zoom in/out anywhere, rotate the map orientation, or change the pitch (angle).
1. **See detailed itineraties** (including timestamps and different modes of transit) by clicking the "Details" link.

Here's a demo:

<img src="img/demo.gif" alt="GIF demo showing how a user can toggle through various maps and view the detailed itinerary" width="300"/>

## Why did I build this?

When I decided to take a group of high school students on 5 bike rides in 5 days, I started wondering how I could communicate the ride itineraries to students (and families/guardians) in an accessible way. 

I set these goals for my product:

1. Families/guardians should **have detailed knowledge** of higher-risk student activities.
2. Students should **practice engaging** with visualized spatial data to **independently answer their own questions** about each day's ride location, duration, elevation, Points of Interest, or itinerary.

## Tech stack

To build this app, I used the following tools:

1. [Google My Maps](https://www.google.com/maps/d/u/0/), for generating the route lines, and exporting the geometries in `KML` format.
1. [togeojson](https://www.npmjs.com/package/@mapbox/togeojson) to convert `KML` files into `geoJSON`.
2. [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/guides) library, for styling and displaying maps and route lines, and adding camera behaviors (flyto animations).
3. [Google Sheets](https://docs.google.com/spreadsheets), for planning and line-by-line itineraries (including formulas to calculate durations), and publishing a single tab as an htm file.
4. [Visual Studio Code](https://code.visualstudio.com/download) free IDE, with [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) and [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extensions.
5. [GitHub pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site), for publishing the app for free!

## Feature Spotlight

One key feature I want to spotlight is the exaggerated terrain. 

If you look closely at the map, you might notice that the hills and mountains are very pronounced. That's because I exaggerated the apperance of topography by 250%. Here's how I did it:

Following [this example](https://docs.mapbox.com/mapbox-gl-js/example/add-terrain/), I first added [this](https://docs.mapbox.com/data/tilesets/reference/mapbox-terrain-dem-v1) Mapbox raster tileset `mapbox://mapbox.mapbox-terrain-dem-v1` to the map as a source. This tileset contains a Digital Elevation Model (DEM) encoded in the RGB values. So, by using `.setTerrain`, we can use the elevation values in the tileset to enable topographical extrusion – to make the map 3D!

So, why 250%? Well, what's the point of adding subtle (realistic) terrain, when my goal is to **prepare students to face some aggressive climbs**? _Those hills should look as mean as they feel._

Check it out:

![terrain eggageration code](img/terrain-code.png)

<img src="img/demo-3d-terrain.gif" alt="GIF demo showing 3d terrain" />

_Exaggerating the elevation profile makes the map more exciting._

## Contributions

Feel free to copy the code if you want it! Comments are welcome on [this blog post](https://domlet.github.io/posts/bike-the-bay/).
