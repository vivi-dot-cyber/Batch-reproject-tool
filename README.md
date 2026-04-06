# Batch-reproject-tool
ArcPy script tool that batch‑reprojects shapefiles to match a target dataset’s spatial reference.

Overview
This project automates the process of reprojecting multiple shapefiles so they match the spatial reference of a target dataset. The script is designed to run as a custom script tool in ArcGIS Pro, allowing users to select a folder of datasets and a target feature class. Any shapefile that does not already match the target projection is reprojected and saved with _projected appended to its name.
This tool demonstrates batch processing, spatial reference handling, ArcPy geoprocessing, and user‑friendly script tool design.

Key Features
- Reads user inputs directly from the ArcGIS Pro tool dialog
- Extracts the spatial reference of a target dataset
- Loops through all shapefiles in a folder
- Reprojects only those that do not match the target projection
- Appends _projected to output names
- Prints a clean, comma‑separated summary of all reprojected datasets
- Skips datasets already in the correct projection

How the Script Works
Imports
- arcpy — Esri’s Python library for geoprocessing
- os — used for file path handling
Parameters
The script uses two parameters from the script tool:
- Input Folder — the directory containing shapefiles
- Target Dataset — the feature class whose projection will be matched

Spatial Reference Extraction
targetSR = arcpy.Describe(target_dataset).spatialReference

Workspace Setup
arcpy.env.workspace = input_folder
fcs = arcpy.ListFeatureClasses()


ArcPy searches the folder and lists all shapefiles.
Looping Through Datasets
For each feature class:
- Get its spatial reference
- Compare it to the target
- If different, reproject 
  
Output Naming
The script removes .shp and appends _projected.shp:
CityBoundaries_projected.shp

Reprojection
arcpy.Project_management(fc, outPath, targetSR)


Result Tracking
All projected datasets are stored in a list and printed as a single summary message.


