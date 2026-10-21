# Poaching Incident Density Analysis in Tanzania

## Problem / Research Question

Where are poaching incidents concentrated in Tanzania, and which visualization
technique best reveals the spatial patterns that are hidden in a raw table of
latitude and longitude values?

Poaching is a serious threat to wildlife, but a plain table of incident records
does not make it easy to see where incidents cluster. This project uses
geographic visualization to turn 268 incident records into readable maps so
that hotspots and low-activity areas can be identified at a glance.

## Dataset Source and Usage Permissions

The dataset is `poaching_points_cleaned.csv`, containing 268 rows and 6 columns
(`id_report`, `date_report`, `description`, `created_date`, `lat`, `lon`). Each
row is one reported poaching incident in Tanzania.

This file is a course-provided sample dataset from the CISC7204 module
(originally distributed with a Python data-visualization textbook). It is used
here for educational and demonstration purposes only. It contains no personal
data and no access-restricted information.

## Methods and Tools Used

- **Python 3**
- **geoplotlib** for interactive map rendering (dot density, histogram, Voronoi)
- **pandas** for loading and inspecting the data

Three visualization layers are applied to the same dataset:

1. **Dot density plot** — each incident is drawn as a point on an OpenStreetMap
   basemap.
2. **Histogram layer** — the map is divided into bins (`binsize=20`) and shaded
   by the count of incidents in each bin, revealing density hotspots.
3. **Voronoi plot** — the map is partitioned into cells around each point
   (`cmap='Blues_r'`, `max_area=1e5`), highlighting the most concentrated region.

## Key Findings

- Poaching incidents are **not evenly distributed** across Tanzania; they
  cluster in a small number of areas, which the raw table alone cannot reveal.
- The dot density plot immediately shows that some areas have far more
  incidents than others.
- The histogram layer makes the hotspots explicit and also highlights areas
  with no incidents at all.
- The Voronoi plot draws attention to one particularly dense region (a large
  dark-blue area near the centre-right of the map) that is easy to miss in the
  other two plots.

**One limitation:** the dataset has only 268 records, so it is a small sample
and may not reflect the full national picture of poaching activity. The maps
also depend on geoplotlib's older rendering stack, which can make reproduction
slightly more involved than with modern libraries such as Plotly or Folium.

## Instructions for Running the Analysis

1. Clone this repository.
2. Create and activate a Python environment and install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

   > Note: `geoplotlib` is a legacy library (last released in 2016). It runs
   > best with Python 3.11 or earlier and an older `pyglet` version. If you use
   > Python 3.12+, you may need to install `pyglet<2` and apply small
   > compatibility patches.

3. Run the notebook `poaching_density_analysis.ipynb` from top to bottom. Each
   call to `geoplotlib.show()` opens an interactive map window for the
   corresponding layer.

The three finished maps are also saved as static images in the
`visualizations/` folder for quick reference.
