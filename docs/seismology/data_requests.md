# Data Requests

## Mass Downloaders

### Stream2segment (GFZ)

    https://github.com/rizac/stream2segment/blob/master/README.md

Zaccarelli, R., Bindi, D., Strollo, A., Quinteros, J., & Cotton, F. (2019). Stream2segment:
An Open‐Source Tool for Downloading, Processing, and Visualizing Massive Event‐Based Seismic
Waveform Datasets. Seismological Research Letters, 90(5), 2028. http://doi.org/10.1785/0220180314.


### obspyDMT (Oxford)

    https://github.com/kasra-hosseini/obspyDMT

Hosseini, K., & Sigloch, K. (2017). ObspyDMT: a Python toolbox for retrieving and processing
large seismological data sets. Solid Earth, 8(5), 1047–1070. http://doi.org/10.5194/se-8-1047-2017


### ObsPy mass_downloader module

    https://docs.obspy.org/packages/autogen/obspy.clients.fdsn.mass_downloader.html

    obspy.clients.fdsn - FDSN Web service client for ObsPy

    https://docs.obspy.org/packages/obspy.clients.fdsn.html

Good for complex or larger queries:

    obspy.clients.fdsn.mass_downloader (for multiple data centers)

## FDSNWS


Using web services: FDSNWS & IRISWS

### Station data (FDSNWS)

    http://service.iris.edu/fdsnws/station/1/query?...

Type http_request_string in a web browser or use `wget` or `curl` from command line

    $ wget -O output_file "http_request_string"

(quotation marks are important to avoid that the shell interprets special characters)

Use HTTP POST

All of the parameters that can be submitted with the GET method are allowed in POST
with the following exceptions: startbefore, endbefore, startafter, endafter

    $ wget --post-file=post_request_file -O output_file http://service.iris.edu/fdsnws/station/1/query

Example of post_request_file:

    level=channel
    format=text
    TA A25A -- BH? 2010-03-25T00:00:00 2010-04-01T00:00:00
    IU ANMO * BH? 2010-03-25T00:00:00 2010-04-01T00:00:00
    IU ANMO 10 HHZ 2010-03-25T00:00:00 2010-04-01T00:00:00
    II KURK 00 BH? 2010-03-25T00:00:00 2010-04-01T00:00:00

In general:

    parameter=<value>
    parameter=<value>
    parameter=<value>
    <network> <station> <location> <channel> <starttime> <endtime>
    <network> <station> <location> <channel> <starttime> <endtime>
    ...


### Event data (FDSNWS)

    http://service.iris.edu/fdsnws/event/1/query?...

This service will not be offered long term, so it is better to go directly to ISC/NEIC

### Waveform data (FDSNWS)

    http://service.iris.edu/fdsnws/dataselect/1/query?...

Same options:

- type URL in web browser (small requests)
- wget/curl (automated or scripted requests)
- HTTP POST (automated or scripted requests)

    quality=<D|R|Q|M|B>
    minimumlength=<seconds>
    longestonly=<true|false>
    <Network> <Station> <Location> <Channel> <StartTime> <EndTime>
    ...

### Waveform data (IRISWS)

    http://service.iris.edu/irisws/timeseries/1/query?...

accepts HTTP POST?

Signal processing options:

+ high, low and band-pass filter
+ remove mean value
+ scaling by constant value
+ deconvolution of instrument response (with frequency limits and unit conversion)
+ differentiation and integration
+ decimation to lower sample rates

- good for complex or large queries


### Other IRIS web services


- `fedcatalog`: A service for federating requests for channel metadata across multiple data centers

- `syngine`: A service for synthetic seismograms

- `timeseriesplot`: A charting webservice offering timeseries graphic display in single-line or helicorder styles

- `rotation`: rotate waveform data into alternate coordinate system

- `sacpz`: instrument response information (per channel)

- `resp`: channel response information

- `evalresp`: instrument response information evaluated from IRIS metadata

- `virtualnetwork`: list of stations in a virtual network

- `traveltime`: travel times and ray parameters for seismic phases using a 1-D spherical earth model

- `flinnengdahl`: a Flinn-Engdahl region code or name for a latitude, longitude pair

- `distaz`: distance, azimuth and back-azimuth between two locations

- `metadatachange`: changes made to SEED metadata

## Other tools

### JWEED

JWEED and other IRIS software use web services

### Fetch scripts

FetchData-2016.089.txt
FetchEvent-2014.340.txt
FetchMetadata-2014.316.txt
FetchSyn-2016.007.txt

Advantages:

- access to other data centers (see -F option)
- can read from BREQ_FAST file
