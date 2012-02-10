MapDig - generic map explorer for CartoDB
========================================
Generate a simple map explorer for CartoDB public tables.

* [Explore your public tables](http://vizzuality.github.com/mapdig/index.html)
* [Explore OpenStreetMap London Points of Interest](http://vizzuality.github.com/mapdig/osm_point.html)
* [Explore OpenStreetMap London Lines](http://vizzuality.github.com/mapdig/osm_line.html)
* [Explore OpenStreetMap London Polygons](http://vizzuality.github.com/mapdig/osm_polygon.html)
* [Explore the 2010 World Database of Protected Areas](http://vizzuality.github.com/mapdig/wdpa.html)

<img src="http://dl.dropbox.com/u/193220/CartoDB/mapdig.png" width="900px"/>

Requirements
------------------

* The cartodb-gmapsv3 map library
* A CartoDB user name.
* A **public** table name.

Example
-------
```Javascript
var carto_user = prompt("Please enter your CartoDB username");
var table      = prompt("Please enter the table to explore");
var ignore     = [];          // columns you don't want to include in your GUI
var width      = 300;         // width of your GUI in pixels
var mapdig     = new MAPDIG.create(carto_user, table, ignore, width);

// initialise the google map
var map = new google.maps.Map(document.getElementById('map_canvas'), {
  center: new google.maps.LatLng(20,0),
  zoom: 3,
  mapTypeId: google.maps.MapTypeId.ROADMAP,
  mapTypeControl: false
});

// initialize the CartoDB layer (see: https://github.com/Vizzuality/cartodb-gmapsv3)
var cartodb1_gmapsv3 = new google.maps.CartoDBLayer({
  map_canvas: 'map_canvas',
  map: map,
  user_name: mapdig.carto_user,
  table_name: mapdig.table,
  query: mapdig.SQL,
  auto_bound: true,
  map_style: true,
});

// initialize the generic GUI
mapdig.init(cartodb1_gmapsv3);
```

