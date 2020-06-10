====================
Providing your Data
====================

Data can be supplied to the GIP in 3 ways

- Providing GIS data (GeoPackage) to EGDI
- Hosting your own OGC Web Services
- Providing secure Database access

Hostng Webservices
-------------------

Hardware Requirements
^^^^^^^^^^^^^^^^^^^^^^

Suggested Software
^^^^^^^^^^^^^^^^^^

Providing GIS Data
------------------

The preferred format to provide data is GeoPackage.

The best support to provide GeoPackage is using QGIS 3.XX.

Create Geopackage
^^^^^^^^^^^^^^^^^

ArcMap
""""""""

1. Create SQLite DB - https://desktop.arcgis.com/en/arcmap/10.4/tools/data-management-toolbox/create-sqlite-database.htm 
2. Choose as spatial_type parameter GEOPACKAGE which will create an OGC GeoPackage dataset. This is essentially an SQLite database with ST_Geometry storage plus some extra OGC features.

You can use this workspace very much like any SQLite geodatabase, that is load/export feature classes and tables and create views. 

Example: Load ESRI GeoDatabase to sqlite - https://tereshenkov.wordpress.com/2016/12/17/load-esri-geodatabase-tables-into-sqlite/ 

If you have raster data you can use the tool - https://desktop.arcgis.com/en/arcmap/latest/tools/conversion-toolbox/add-raster-to-geopackage.htm 

ArcPro
"""""""

For overview - https://community.esri.com/community/open-platform-standards-and-interoperability/blog/2019/08/14/how-can-i-use-ogc-geopackages-in-arcgis-pro 

"Move your data into the GeoPackage like this:

1. Create a GeoPackage with the Create SQLite Database tool (using the GeoPackage spatial type)
2. Use the Copy tool (Data Management, General toolset) to add vector data, or Copy/Paste in the Catalog pane
3. Use the Add Raster to GeoPackage tool (Conversion, To GeoPackage toolset) to add raster mosaics

Your GeoPackage is now ready for use."

QGIS
""""""

1. Download QGIS 3.8
2. Import current data
3. Make any styling changes required
4. Open the processing toolbox (Ctrl+Alt+T)
5. Open "Database" menu
6. Select "Package Layers"
7. Select input layers to package (3 dot button on right)
8. Make sure "Save Layer Styles into GeoPackage" is selected
9. Choose filename and destination of final geopackage
10. Click Run

Should now find your geopackage where ever you selected to save it. Drag and drop it into a new QGIS window to check it's output is as expected.

GDAL
""""""

1. Download GDAL
2. Check it has GeoPackage support using `ogrinfo --formats`

You should have something like `GPKG -raster,vector- (rw+vs): GeoPackage`

and also check that your input file format is listed

3. You can check what options you have to create a GPKG with:

`ogrinfo --format GPKG`

Help on options for GeoPackage can can be found at:

https://gdal.org/drivers/vector/gpkg.html

and

https://gdal.org/drivers/raster/gpkg.html

and

https://gdal.org/programs/ogr2ogr.html

4. use `ogr2oger` to create and update your GeoPackage

For example to add a directory of shapefiles use:

`ogr2ogr -f "GPKG" filename.gpkg ./path/to/dir`

and to add data to this geopackage (say from an Oracle table) you could use:

`ogr2ogr -f "GPKG" filename.gpkg oraSource.ovf -nln my_new_layer_name -update"`

Where `oraSource.ovf` is a virtual layer containing information about the Oracle database like:

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <OGRVRTDataSource xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:noNamespaceSchemaLocation="http://ogc2.bgs.ac.uk/xs/ogrvrt.xsd">
        <OGRVRTLayer name="mintell">
            <SrcDataSource>OCI:USER/Password@//host:port/sid</SrcDataSource>
            <SrcSQL>
                SELECT *
                FROM PUBLISHED.XXX
            </SrcSQL>
            <GeometryType>wkbNone</GeometryType>
        </OGRVRTLayer>
    </OGRVRTDataSource>

Providing Web Services
----------------------

We will try to assist with the setup of web services to serve data to EGDI,
by providing a basic explanation of how to do so easily.

WMS
^^^^

- Be awesome
- Make things faster

WFS
^^^

Install $project by running:

    install project

WCS
^^^^

- Issue Tracker: github.com/$project/$project/issues
- Source Code: github.com/$project/$project

Support
-------

If you are having issues, please let us know.
email: support@geoera.eu
Issue Tracker: https://github.com/GeoEra-GIP/Project-Support-WP8
