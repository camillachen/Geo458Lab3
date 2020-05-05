# Xiao Ye Chen Geo458 Lab 3: Web Map Design
### About the functions
The functions I used are the

The function that changes the color of the icons (paper plane icons) is:
<pre><code>pointToLayer: function (feature, latlng) {
            var id = 0;
            if (feature.properties.CNTL_TWR == "Y") { id = 0; }
            else if (feature.properties.CNTL_TWR == "N")  { id = 1; }
            return L.marker(latlng, {icon: L.divIcon({className: 'fa fa-paper-plane marker-color-' + (id + 1).toString() })});
        }
</code></pre>
It is done by assigning an id to a color based on if the airport has air traffic control tower.

The other function I used is:
<pre><code>
onEachFeature: function (feature, layer) {
    layer.bindPopup(feature.properties.AIRPT_NAME);
}
</pre></code>
Which makes it so that when the user click on any paper plane icon, it will display the airport name as a popup.

The other function I used is:
<pre><code>
function setColor(density) {
    var id = 0;
    if (density > 18) { id = 4; }
    else if (density > 13 && density <= 18) { id = 3; }
    else if (density > 10 && density <= 13) { id = 2; }
    else if (density > 5 &&  density <= 10) { id = 1; }
    else  { id = 0; }
    return colors[id];
}
</pre></code>

and what that does is change the density of the color of the shade of the state fill in color depending on the number of airports in the state. The more airport the state has, the more "dense" the color will be, which is darker shade and vice versa for states with less airports.

<pre><code>
function style(feature) {
    return {
        fillColor: setColor(feature.properties.count),
        fillOpacity: 0.4,
        weight: 2,
        opacity: 1,
        color: '#b4b4b4',
        dashArray: '4'
    };
}
</pre></code>
This gives the color of the state based on the count of airports in the state, which is also the airport density.

This function gives information to the legend on my map.
<pre><code>
legend.onAdd = function () {

    // Create Div Element and Populate it with HTML
    var div = L.DomUtil.create('div', 'legend');
    div.innerHTML += '<b># Airports</b><br />';
    div.innerHTML += '<i style="background: ' + colors[4] + '; opacity: 0.5"></i><p>19+</p>';
    div.innerHTML += '<i style="background: ' + colors[3] + '; opacity: 0.5"></i><p>14-18</p>';
    div.innerHTML += '<i style="background: ' + colors[2] + '; opacity: 0.5"></i><p>11-13</p>';
    div.innerHTML += '<i style="background: ' + colors[1] + '; opacity: 0.5"></i><p> 6-10</p>';
    div.innerHTML += '<i style="background: ' + colors[0] + '; opacity: 0.5"></i><p> 0- 5</p>';
    div.innerHTML += '<hr><b>Has air traffic control tower?<b><br />';
    div.innerHTML += '<i class="fa fa-paper-plane marker-color-1"></i><p>Yes control tower</p>';
    div.innerHTML += '<i class="fa fa-paper-plane marker-color-2"></i><p>No control tower</p>';
    // Return the Legend div containing the HTML content
    return div;
};
</pre></code>

This will populate the legend with number of airports and it will show the color based on the colors I've had before showing how many airports are in each state.
There is also another part of the legend that shows if the airport has a air traffic control tower based on the color of the paper plane icon.

### About the map

  The map displays all the airports in the United States with a paper plane icon since there are planes in airports.

 The green colored planes have an air trafic control tower and the orange one does not, as shown in the legend on the top right.

 The states are separated by different colors depending on how many airports they have in that state. The darker the shade is, the more airpoprts the states have, and the lighter the shade of the state is, the less airport the states has, also shown in the legend on the top right.

 If you click on a paper plane icon, it will tell you the name of that airport, so it is an interactive map.


#### The Source
>The libraries I used are the airports.geojson and the us-states.geojson.
* The source for the airports.geojson data that shows all the airports in the United States is from [data.gov](https://catalog.data.gov/dataset/usgs-small-scale-dataset-airports-of-the-united-states-201207-shapefile).
* The source for the us-states.geojson data that shows the boundaries of all the states in the United States is from [Mike Bostock](https://bost.ocks.org/mike/).
* The basemap I used is from [CartoDB](http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png).
* The paper plane icon is from [Font Awesome](https://fontawesome.com/).
* The font I used is called the [Titillium Web](https://fonts.googleapis.com/css?family=Titillium+Web).
* The Map is made by me (Xiao Ye Chen).
