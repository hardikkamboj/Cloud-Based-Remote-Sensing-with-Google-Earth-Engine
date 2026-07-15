# Assignment Questions 

### Assignment 1. Recall the plots of spectral resolution we created for MODIS and EO-1. Create a plot of spectral resolution for one of the other sensors described in this chapter. What are the bands called? What wavelengths of the electromagnetic spectrum do they correspond to?
```
`var tmBands = tmImage.bandNames();

// Print the list.
print(tmBands);


var reflectanceImageTm = tmImage.select(
    'B1',
    'B2',
    'B3',
    'B4',
    'B5',
    'B6',
    'B7'
);

var options = {
    title: 'TM spectrum at SFO',
    hAxis: {
        title: 'Band'
    },
    vAxis: {
        title: 'Reflectance'
    },
    legend: {
        position: 'none'
    },
    pointSize: 3
};

// Make the chart.
var tmReflectanceChart = ui.Chart.image.regions({
    image: reflectanceImageTm,
    regions: sfoPoint
}).setOptions(options);

// Display the chart.
print(tmReflectanceChart);

```

### Assignment 2. Recall how we extracted the spatial resolution and saved it to a variable. In your code, set the following variables to the scales of the bands shown in Table 4.1.
```
var modisB01Scale = modisImage.select('sur_refl_b01')
    .projection().nominalScale();

var msiB5Scale = msiImage.select('B5')
    .projection().nominalScale();
print('MSI scale:', msiScale);


var naipScale = naipImage.select('R')
    .projection().nominalScale();

print('NAIP NIR scale:', naipScale);

```
    

### Make this point in your code: ee.Geometry.Point([-122.30144, 37.80215]). How many MYD09A1 images are there in 2017 at this point? Set a variable called mod09ImageCount with that value, and print it. How many Sentinel-2 MSI surface reflectance images are there in 2017 at this point? Set a variable called msiImageCount with that value, and print it.



```


// Define a region of interest as a point at San Francisco airport.
var point = ee.Geometry.Point([-122.30144, 37.80215]);

// Center the map at that point.
Map.centerObject(point, 16);

var mod09ImageCount = mod09
    .filterBounds(point)
    .filterDate('2017-01-01', '2018-01-01')
    .size();
print('MYD09A1 images in 2017:', mod09ImageCount);

// Sentinel-2 MSI surface reflectance images in 2017 at the point
var msiImageCount = msi
    .filterBounds(point)
    .filterDate('2017-01-01', '2018-01-01')
    .size();
print('MSI images in 2017:', msiImageCount);

```
