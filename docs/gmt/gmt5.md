# GMT5

Recipes for GMT5

## Initial configuration

    $ gmt defaults > gmt.conf

Reduce fonts sizes (defaults too large)

    #
    # FONT Parameters
    #
    FONT_ANNOT_PRIMARY             = 10p,Helvetica,black
    FONT_ANNOT_SECONDARY           = 12p,Helvetica,black
    FONT_LABEL                     = 14p,Helvetica,black
    FONT_LOGO                      = 8p,Helvetica,black
    FONT_TITLE                     = 14p,Helvetica,black


Set map frame to plain

    MAP_FRAME_TYPE                 = plain


## Specifying line sytle

Line style is specified with the `-W` option:

```
    -Wwidth,color,style
```

Values of `width` can be: `thinnest` (0.25p), `thinner` (0.5p), `thin` (0.75p), or `thick` (1p).

- `color` can be specified with name or R/G/B

- `style`:
    - `dotted` or `.`
    - `dashed` or `-`
    - `.-`
    - `string:offset` (e.g. `4_8_5_8:2p`)

## pstext format

    $ gmt pstext -J -R -F+f12p,Helvetica,black+jLB -W1.5p -G255 -K -O

f: 12p font size
   Helvetica font
   black color
j: theJustify LB (left bottom)

a: angle

-W1.5p = outline
-Gwhite (255) = box background

-D0.3/0.3  = add offset from x,y coordinates (e.g. lower left corner)

## psscale format

    $ gmt psscale -Cvp.cpt -Dx8c/-1c+w12c/0.5c+jTC+h+e -Bx+l"label"

x8c/-1c = plot scale at fixed plot coordinates 8c/1c
w12c/0.5c = scale size is 12c long by 0.5c wide
jTC = justification is top-center
h = plot a horizontal scale
e = plot end triangles

## Close a GMT Postscript file

    $ gmt psxy -R -J -T -O >> $psfile

## Set label with decimal degrees 

    gmt set FORMAT_GEO_MAP             ddd.xF


## New label format

    -B[p|s][x|y|z][a|f|g]<tick>[m][l|p]
    -B[p|s][x|y|z][+l<label>][+p<prefix>][+u<unit>]
    -B[<axes>][+b][+g<fill>][+o<lon>/<lat>][+t<title>]

Examples:

    -Bxa${xa}f${xt}g${xg} -Bya${ya}f${yt}g${yg}${axis} -BWeSn+t"${label}"

    -Bxa${xa}f${xt}g${xg}+l"x label" -Bya${ya}f${yt}g${yg}+l"y label" -BWeSn+t"${label}"

## Make water semitransparent

    gmt pscoast ... -S200 -t30

Then must convert to pdf in order to see transparency

## Pens, transparency, etc (not tested!!!!)

-W0.25p+s : interpolates curve with splines!

-t : transparency for this layer (command?). Only visible in PDF format => use psconvert
0 = opaque
100 = fully transparent

chech PS_TRANSPARENCY in gmt.def
color or fill specifications may append @transparency to change the PDF transparency level


## Convert shapefile to GMT

Directly:

    $ org2ogr -f “GMT” output.gmt input.shp

In two steps (in case direct conversion gives an error, e.g. Vectors not supported)

    $ ogr2ogr -f “KML” example.kml example.shp
    $ org2ogr -f “GMT” example.gmt example.kml


## gmt2kml

Simple symbols:

    awk '{print $3, $2}' stafile | \
    gmt gmt2kml -Gfred -Fs -I$icon -T"Title" > stations.kml

Symbols with labels:

    awk '{print $3, $2}' stafile | \
    gmt gmt2kml -Gfred -Fs -N- -I$icon -T"Title" > stations.kml

    awk '{print $3, $2}' stafile | \
    gmt gmt2kml -Fs -Sc1.5 -Gfgreen -I$icon -N- -Sn0.8 -Gnpink -T"Title" > stations.kml


-Fs -Sc1.5 -Gfgreen: plot symbol (x,y in file), size and fill

-N- -Sn0.75 -Gngray: label in 3rd column, size (relative to 1), fill color

-Gn- : turn off labels [works?]

-Fs = symbol   : x y [label]

-Fe = event    : x y [label] time

-Ft = timespan : x y [label] tstart tstop/"NaN"

-Fl = line

-Fp = polygon

-Fw = wiggle

For stations/OBSs one could use -As0.0 to get altitude "Clamped to sea floor/ground" [works?]
(see https://developers.google.com/kml/documentation/altitudemode)

For **Clamped to sea floor** to work must change:

    <kml xmlns="http://www.opengis.net/kml/2.2">

with:

    <kml xmlns="http://www.opengis.net/kml/2.2"
            xmlns:gx="http://www.google.com/kml/ext/2.2">

To get rid of subfolders in kml file, comment or delete everything between </Style> and first <Placemark>:

```
</Style>
  <Folder>
    <name>stdin</name>
    <Folder>
      <name>Point Set 0</name>
        <Placemark>
```

and also closing tags </Folder>


List of Google Maps icons:

- [triangle](http://maps.google.com/mapfiles/kml/shapes/triangle.png)
- [donut](http://maps.google.com/mapfiles/kml/shapes/donut.png)
- [square](http://maps.google.com/mapfiles/kml/shapes/square.png)
- [open-diamond](http://maps.google.com/mapfiles/kml/shapes/open-diamond.png)
- [polygon](http://maps.google.com/mapfiles/kml/shapes/polygon.png)
- [star](http://maps.google.com/mapfiles/kml/shapes/star.png)
- [target](http://maps.google.com/mapfiles/kml/shapes/target.png)
- [volcano](http://maps.google.com/mapfiles/kml/shapes/volcano.png)
- [earthquake](http://maps.google.com/mapfiles/kml/shapes/earthquake.png)
- [placemark_circle](http://maps.google.com/mapfiles/kml/shapes/placemark_circle.png)
- [placemark_circle_highlight](http://maps.google.com/mapfiles/kml/shapes/placemark_circle_highlight.png)
- [placemark_square](http://maps.google.com/mapfiles/kml/shapes/placemark_square.png)
- [placemark_square_highlight](http://maps.google.com/mapfiles/kml/shapes/placemark_square_highlight.png)
