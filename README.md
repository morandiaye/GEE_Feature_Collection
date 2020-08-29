# GEE_Feature_Collection
## 1. Import feature colection
This feature is made up of department of senegal
```js
var departement = ee.FeatureCollection("users/ndmorndiaye/senegal_dep");
```
## 2. Make function to compute area in km2
```js
// add area of department km2
var sup=function(feature){
  return ee.Feature(feature).set({areaha:feature.geometry().area().divide(1000*1000)
})};
```
## 3. Spread function in all feature collection
```js
// Spread on all feature in collection feature feature
var dep_new=departement.map(sup);
// take a look in change i made
print("new departement",dep_new);
```
## 4. Add Centroids in the feature collection : departement
```js
var centroid=function(feature){
  var prop=["DEPT","REG","STATUT","areaha"]
  return ee.Feature(feature.geometry().centroid()).copyProperties(feature,prop)
};

```
## 5. Applicate function over all feature in dep_new
```js
// Applicate the fuction in all fearture collection
var dep_centroids=dep_new.map(centroid);
print("centroids:",dep_centroids);
```
## 6. Data vizualization
```js
Map.centerObject(departement,6)
Map.addLayer(ee.Image().paint(departement,"black",1),{},"Limit Department")
Map.addLayer(dep_centroids,{},"departement centroids");

```
link:[earth engine link](https://code.earthengine.google.com/cfebbf00cd601bbfcec9e3e7757236d0)
