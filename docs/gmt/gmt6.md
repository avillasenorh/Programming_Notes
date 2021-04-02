#GMT6


## Differences to previous versions

- Modern mode
- Default: use `.nc` extension for netCDF grids instead of old-style native grid format `.grd`

## initial configuration

    $ gmt defaults -D > ~/gmt.conf

Reduce fonts sizes (defaults too large)

    #
    # FONT Parameters
    #
    FONT_ANNOT_PRIMARY             = 10p,Helvetica,black
    FONT_ANNOT_SECONDARY           = 12p,Helvetica,black
    FONT_LABEL                     = 14p,Helvetica,black
    FONT_TITLE                     = 14p,Helvetica,black

Set map frame to plain

    MAP_FRAME_TYPE                 = plain


## Earth Relief Grids

GMT6 global earth relief grids
[page](https://docs.generic-mapping-tools.org/latest/datasets/remote-data.html#global-earth-relief-grids).

To extract topography/bathymetry of a region:

    $ gmt grdcut @earth_relief_rru -Rlon1/lon2/lat1/lat2 -Goutput.nc

u = s for seconds, m for minutes, d for degrees

- 01s = SRTM1S (30 m)
- 03s = SRTM3S (90 m)
- 15s = SRTM15+V2 (Tozer et al., Earth Space Sci., 2019) (~450 m)

The rest are downsampled versions of 15s

- 30s =  ~ 1 km
- 1m = 1.8 km

With grids >= 15s the global file is downloaded to `~/.gmt/server`.
With grids 03s and 01s, only the tiles inside the region are donwloaded.

To delete all the data in `~/.gmt/server`:

    $ gmt clear data

All global grids are gridline-registered except the 15s that is pixel-registered (check!!)

## File Formats

GMT6 file formats [page](http://gmt.soest.hawaii.edu/doc/latest/GMT_Docs.html#app-file-formats).


### Grid files

Default = netCDF (.nc extension)

