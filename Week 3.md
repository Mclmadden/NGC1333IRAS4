### Monday - 6/24/19

Used CASA's `immoment` command to make moment maps for each of the three peaks shown in `CH3OH_line8` with its FITS file

Found minimum for `includepix` by making an aperture over the `CH3OH_line8` image in CASA Viewer and doubling its root mean squared (RMS):

Center X (hr:min:sec of arc) | Center Y (deg, arcmin, arcsec) | Height x Width | RMS (V)
---|---|---|---
3:29:10.393 | 31, 13, 32.813 | 125 x 125 | 1.682e-3

Based ranges for `chan` off of aperture spectrum peaks:

---| Peak 1 | Peak 2 | Peak 3
---|---|---|---
**Radio Velocity (km/s)** | -4.85372 | 7.17064 | 63.5348 
**Ranges (km/s)** | [-6, -2] | [5, 8] | [61, 65]

```python
casa #will not run if CASA isn't installed

taskname='immoments'
default()
imagename = 'NGC1333IRAS4A_CH3OH_line8.fits'
moments=[0]
chans=('range=[-6km/s,-2km/s]') #First peak radio velocity range
includepix=[3.364e-3, 1e9]
outfile='NGC1333IRAS4A_CH3OH_line8_m0p1.moment'
immoments()

chans=('range=[5km/s, 8km/s]') #Second peak radio velocity range
outfile='NGC1333IRAS4A_CH3OH_line8_m0p2.moment'
immoments()

chans=('range=[61km/s,65km/s]') #Third peak radio velocity range
outfile='NGC1333IRAS4A_CH3OH_line8_m0p3.moment'
immoments()
```

Began reading Mark R. Krumholz's *Notes on Star Formation* review

### Tuesday - 6/25/19

Had technical difficulties installing PySpecKit, which would be used to fit a Gaussian to spectrum of `CH3OH_line8` at protostar B1

Wrote code to test when the issue is resolved:

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u

sp = psk.Spectrum('CH3OH_line8_B1.fits') #Reads FITS file into PySpecKit
sp.plotter()

#Fit with input guesses from CASA Viewer spectrum at B1
amplitude_guess = 5.5 * u.mJy/u.beam
center_guess = 6.5 * u.km/u.s
width_guess = 3 * u.km/u.s
guesses = [amplitude_guess, center_guess, width_guess]

sp.specfit(fittype='gaussian', guesses=guesses)
```

Documentation:
>https://pyspeckit.readthedocs.io/en/latest/fitting.html

>https://pyspeckit.readthedocs.io/en/latest/example_fromscratch.html

Read more of Krumholz's *Notes on Star Formation* review

Became familiarized with Overleaf for future reference

### Wednesday - 6/26/19

Read more of Krumholz's *Notes on Star Formation* review

Moved Anaconda to a different directory and successfully downloaded PySpecKit

Tested yesterday's code, and there's an error with the units: `TypeError: only dimensionless scalar quantities can be converted to Python scalars`

Tried automatic guesses to test fitting a Gaussian to data:

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u

sp = psk.Spectrum('CH3OH_line8_B1.fits')
sp.plotter()

sp.specfit(fittype='gaussian')
```

Above code worked, but returned message: `Legend.draggable() is deprecated in favor of Legend.set_draggable(). Legend.draggable may be reintroduced as a property in future releases.`

Troubleshooting instructed to use `self.fitleg.set_draggable(True)` but unsure where to input as straight into `ipython` returns message: `NameError: name 'self' is not defined`

Informed by PySpecKit coauthor Adam Ginsburg that PySpecKit doesn't work with astropy quatities, so guesses must be unitless, and Ginsburg's latest development version resolves the draggable issue: `pip install https://github.com/pyspeckit/pyspeckit/archive/master.zip`

Updated code:

```python
import numpy as np
import pyspeckit as psk

sp = psk.Spectrum('CH3OH_line8_B1.fits')
sp.plotter()

#Amplitude = 5.5 mJy/beam, center = 6.5 km/s, width = 3 km/s
guesses = [5.5, 6.5, 3]

sp.specfit(fittype='gaussian', guesses=guesses)
```

### Thursday - 6/27/19

Plot axes were off because the units need to be converted from velocity to frequency to velocity relative to each methanol transitions' rest frequency

Gaussin fit wasn't appearing because `sp.plotter()` must preceed `sp.specfit()`

Updated code:

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u
import pylab as pl
pl.ion()

sp = psk.Spectrum('CH3OH_line8_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24928.728 * u.MHz)

sp.plotter()
sp.specfit(fittype='gaussian', guesses=[5.5,5,3])

sp.specfit.parinfo #Returns paramters: amplitude, center, width
```

![Plot of `CH3OH_line8`](https://github.com/Mclmadden/repository/NGC1333IRAS4/plot_CH3OH_line8.png)

Splatalogue information for `CH3OH_line15` and `CH3OH_line16` missing

Updated table:

Rest Frequency (MHz) | Frequency Error (MHz) | CDMS/JPL Intensity | Upper Level Energy (K)|---| Quantum Numbers |----------| Symmetry State | Species
---|---|---|---|---|---|---|---|---
  24928.7280  | 0.013  |  -5.9530 3  | 24.3097 | 28 | 325041404 | 3 2 2 1  |   3 1 2 1    |    CH3OH, vt=0-2
  24933.5040  | 0.012  |  -5.8203 3  | 30.7644 | 36 | 325041404 | 4 2 3 1  |   4 1 3 1    |    CH3OH, vt=0-2
  24934.4010  | 0.013  |  -6.1883 3  | 19.4686 | 20 | 325041404 | 2 2 1 1  |   2 1 1 1    |    CH3OH, vt=0-2
  24959.1230  | 0.012  |  -5.7292 3  | 38.8326 | 44 | 325041404 | 5 2 4 1  |   5 1 4 1    |    CH3OH, vt=0-2
  25018.1760  | 0.012  |  -5.6612 3  | 48.5142 | 52 | 325041404 | 6 2 5 1  |   6 1 5 1    |    CH3OH, vt=0-2
  25124.9320  | 0.012  |  -5.6082 3  | 59.8092 | 60 | 325041404 | 7 2 6 1  |   7 1 6 1    |    CH3OH, vt=0-2
  25294.4830  | 0.013  |  -5.5657 3  | 72.7174 | 68 | 325041404 | 8 2 7 1  |   8 1 7 1    |    CH3OH, vt=0-2
  25541.4670  | 0.014  |  -5.5310 3  | 87.2386 | 76 | 325041404 | 9 2 8 1  |   9 1 8 1    |    CH3OH, vt=0-2
  25878.2390  | 0.024  |  -5.3415 3  |  
  26313.0930  | 0.025  |  -5.3186 3  |

Made plots of all methanol files

### Friday - 6/28/19
