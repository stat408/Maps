# Static Maps in R

Creating static maps in R, which ggplot, requires downloading map layers.

## 1. Downloading Map Layers

### ggmap

ggmap is a nice way to download map layers, including satellite images. Unfortunately, `ggmap` now requires a Google Maps API key. The `get_map()` function relies on Google to draw the appropriate map. The API is free up to a reasonable limit, but then does end up costing. To get the key, you'll have to enter credit card information. I do this for my own work, but we will avoid that for classroom examples. If you'd like high resolution base layers for your project, look into this option.

```
library(ggmap)

bozo_map <- get_map(location = 'bozeman')
```

### maps

As we saw with leaflet, we can use the `maps` package to download maps too. There are county, state, and country level maps for the US as well as a few other countries.

```
mt <- map_data("county", "montana")
head(mt)
```


1. Use the MT income dataset to create a choropleth with county population Montana. Do the same for Income

---

```
seattle <- read_csv('http://math.montana.edu/ahoegh/teaching/stat408/datasets/Seattle_911_062016.csv') 
  
wa <- map_data("county", "Washington")
head(wa)

wa |> filter(subregion %in% c('king')) |>
  ggplot( aes(x = long, y = lat)) +
  geom_polygon(aes(group = group), fill = NA, colour = "grey60") +
  theme_minimal() +
  geom_point(data = seattle |> rename(lat = Latitude, long = Longitude), color = 'navy') +
  coord_quickmap() +
  xlab('') +
  ylab('')
```

2. Explore the `geom_density2d` and `geom_density_2d_filled` functions with the seattle 911 calls.


3. Embed a shiny app to create a heat map by a selected factor with the seattle 911 data
