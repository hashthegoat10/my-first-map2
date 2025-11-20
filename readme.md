# My Favorite Places 

!["Bike The Bay" App](img/header.png)

## Overview 

["My Favorite Places" App](https://hashthegoat10.github.io/my-first-map2/)  is a one-page, that shows all of my favorite places 

Here's a demo:

<img src="img/demo.gif" alt="GIF demo showing how a user can toggle through various maps and view the detailed itinerary" width="300"/>

## Code Spotlight

When I decided to take a group of high school students on 5 bike rides in 5 days, I started wondering how I could communicate the ride itineraries to students (and families/guardians) in an accessible way. 

I set these goals for my product:

1. Families/guardians should **have detailed knowledge** of higher-risk student activities.
2. Students should **practice engaging** with visualized spatial data to **independently answer their own questions** about each day's ride location, duration, elevation, Points of Interest, or itinerary.

## Technology

To build this app, I used the following tools:

1. [Google My Maps](https://www.google.com/maps/d/u/0/), for generating the route lines, and exporting the geometries in `KML` format.
1. [togeojson](https://www.npmjs.com/package/@mapbox/togeojson) to convert `KML` files into `geoJSON`.
2. [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/guides) library, for styling and displaying maps and route lines, and adding camera behaviors (flyto animations).
3. [Google Sheets](https://docs.google.com/spreadsheets), for planning and line-by-line itineraries (including formulas to calculate durations), and publishing a single tab as an htm file.
4. [Visual Studio Code](https://code.visualstudio.com/download) free IDE, with [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) and [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) extensions.
5. [GitHub pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site), for publishing the app for free!

