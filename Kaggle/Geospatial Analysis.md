# Geospatial Analysis

- Your First Map

```
import geopandas as gpd
full_data = gpd.read_file("../input/geospatial-learn-course-data/DEC_lands/DEC_lands/DEC_lands.shp") # shapefile
wild_lands = data.loc[data.CLASS.isin(['WILD FOREST', 'WILDERNESS'])].copy()
ax = world.plot(figsize=(20,20),color='whitesmoke',linestyle=':',edgecolor='black')
world_loans.plot(ax=ax,markersize=2)
```

Point, LineString, Polygon

- Coordinate Reference Systems

three-dimensional globe - map projection - coordinate reference system (CRS)

```
print(regions.crs)
facilities = gpd.GeoDataFrame(facilities_df, geometry=gpd.points_from_xy(facilities_df.Longitude, facilities_df.Latitude))
facilities.crs = {'init': 'epsg:4326'}
ax = regions.plot(figsize=(8,8), color='whitesmoke', linestyle=':', edgecolor='black')
facilities.to_crs(epsg=32630).plot(markersize=1, ax=ax) # to_crs() method modifies only the "geometry" column
```

- Interactive Maps

```
# Create the map
m_3 = folium.Map(location=[42.32,-71.0589], tiles='cartodbpositron', zoom_start=13)
# Add points to the map
mc = MarkerCluster()
for idx, row in daytime_robberies.iterrows():
    if not math.isnan(row['Long']) and not math.isnan(row['Lat']):
        mc.add_child(Marker([row['Lat'], row['Long']]))
m_3.add_child(mc)
# Display the map
m_3
```

```
# Add a bubble map to the base map
for i in range(0,len(daytime_robberies)):
    Circle(
        location=[daytime_robberies.iloc[i]['Lat'], daytime_robberies.iloc[i]['Long']],
        radius=20,
        color=color_producer(daytime_robberies.iloc[i]['HOUR'])).add_to(m_4)
```

```
# Add a heatmap to the base map
HeatMap(data=crimes[['Lat', 'Long']], radius=10).add_to(m_5)
```

```
# GeoDataFrame with geographical boundaries of Boston police districts
districts_full = gpd.read_file('../input/geospatial-learn-course-data/Police_Districts/Police_Districts/Police_Districts.shp')
districts = districts_full[["DISTRICT", "geometry"]].set_index("DISTRICT")
# Number of crimes in each police district
plot_dict = crimes.DISTRICT.value_counts()
# Add a choropleth map to the base map
Choropleth(geo_data=districts.__geo_interface__, 
           data=plot_dict, 
           key_on="feature.id", 
           fill_color='YlGnBu', 
           legend_name='Major criminal incidents (Jan-Aug 2018)'
          ).add_to(m_6)
```

- Manipulating Geospatial Data

Geocoding: Geocoding is the process of converting the name of a place or an address to a location on a map.

```
geolocator = Nominatim(user_agent="kaggle_learn")
location = geolocator.geocode("Pyramid of Khufu")
print(location.point)
print(location.address)
```

```
def my_geocoder(row):
    try:
        point = geolocator.geocode(row).point
        return pd.Series({'Latitude': point.latitude, 'Longitude': point.longitude})
    except:
        return None
universities[['Latitude', 'Longitude']] = universities.apply(lambda x: my_geocoder(x['Name']), axis=1)
universities = universities.loc[~np.isnan(universities["Latitude"])]
universities = gpd.GeoDataFrame(
    universities, geometry=gpd.points_from_xy(universities.Longitude, universities.Latitude))
universities.crs = {'init': 'epsg:4326'}
```

Table Joins

1. Attribute join: use pd.DataFrame.join() to combine information from multiple DataFrames with a shared index (by simpling matching values in the index).

```
europe = europe_boundaries.merge(europe_stats, on="name")
```

2. Spatial join:  With a spatial join, we combine GeoDataFrames based on the spatial relationship between the objects in the "geometry" columns.

```
# Use spatial join to match universities to countries in Europe
european_universities = gpd.sjoin(universities, europe)
```

- Proximity Analysis

Measuring distance

```
# Select one release incident in particular
recent_release = releases.iloc[360]
# Measure distance from release to each station
distances = stations.geometry.distance(recent_release.geometry)
```

Creating a buffer

```
two_mile_buffer = stations.geometry.buffer(2*5280)
GeoJson(two_mile_buffer.to_crs(epsg=4326)).add_to(m)
# Turn group of polygons into single multipolygon
my_union = two_mile_buffer.geometry.unary_union
# The closest station is less than two miles away
my_union.contains(releases.iloc[360].geometry)
```
