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
