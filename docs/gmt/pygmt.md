# pyGMT


## Common usage

```python
import pygmt

fig = pygmt.Figure()

fig.coast(region='g', projection='R20/8i', shorelines=True,
          water='ligthblue', land='gray', frame=True, resolution='i')

fig.show()                                   # for notebooks
fig.show(method='external')                  # output in Preview
```

How to set plotting region:

```python
region = [45, 55, 135, 145]     # rectangular region
region = 'g'                    # globe
region = 'EG'                   # country (Egypt)
```

```python
fig.plot(x=, y=, style='a0.2i', color='red', pen='black', label=f'red')

frame=True
frame=0        # also False?
frame='a5f1'
```

If the data are labelled:

    fig.legend()       # plots a legend similar to Matplotlib


## Pass arguments to a Figure method

```python
KWARGS = dict(grid='@earth_relief_10m', region='g', projection='R-130/5i', frame=0, )

fig = pygmt.Figure()
fig.grdimage(**KWARGS)

fig.grdimage(shading=True, **KWARGS)
```


`grdimage` can also use an object to plot (not necessarily a file name):

```python
import xarray as xr
data = xr.DataArray(....)

fig.grdimage(data, fname=True, ..., cmap='inferno', Q=True) # Q=True in NaN make it transparent

fig.colorbar(frame='+l"velocity"')
```

## Modules not available in pyGMT:

```python
with pygmt.clib.Session() as session:
    session.call_module('meca', f'all the options here')
```

there is a trick to create a temporary file, use it and delete it.

```python
with pygmt.helpers.GMTTempFile() as temp_file:
    with open(temp_file.name, 'w') as f:
        f.write('vaules')
    with pygmt.clib....
        uset temp_file.name in arguments to session.call_module(....)
```

