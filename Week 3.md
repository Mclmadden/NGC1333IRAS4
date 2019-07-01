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

sp = psk.Spectrum('CH3OH_line10_B1.fits') #Reads in methanol FITS file
sp.xarr.convert_to_unit(u.MHz) 
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24959.1230*u.MHz) 

sp.plotter(title='CH3OH_line10', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam') #Makes plot 
sp.specfit(fittype='gaussian', guesses=[5.5,5,3]) #Fits Gaussian to plot

sp.specfit.parinfo #Returns paramters: amplitude, center, width
```

Plot of `CH3OH_line10`:
![plot_CH3OH_line10](https://user-images.githubusercontent.com/23585856/60352618-6ffc0c00-9985-11e9-9e03-c8d26fe7077f.png)

Splatalogue information for `CH3OH_line15` and `CH3OH_line16` missing:

Methanol File | Rest Frequency (MHz) 
---|---
 CH3OH_line15 | 25878.2390 
 CH3OH_line16 | 26313.0930 

Made plots with Gaussian fits of all methanol files at protostar B1:

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u
import pylab as pl
pl.ion()

sp = psk.Spectrum('CH3OH_line8_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24928.728*u.MHz) 
sp.plotter(title='CH3OH_line8', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line10_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24959.123*u.MHz) 
sp.plotter(title='CH3OH_line10', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line11_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25018.176*u.MHz) 
sp.plotter(title='CH3OH_line11', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line12_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25124.932*u.MHz) 
sp.plotter(title='CH3OH_line12', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line13_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25294.483*u.MHz) 
sp.plotter(title='CH3OH_line13', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line14_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25541.467*u.MHz) 
sp.plotter(title='CH3OH_line14', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line15_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25878.239*u.MHz) 
sp.plotter(title='CH3OH_line15', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])

sp = psk.Spectrum('CH3OH_line16_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=26313.093*u.MHz) 
sp.plotter(title='CH3OH_line16', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3])
```

### Friday - 6/28/19

Read more of Krumholz's *Notes on Star Formation* review

Gaussian fit errors are all drastically off most likely because the fitter thinks the data noise is greater than it actually is

Used Doppler Equation to calculate the velocity offsets of the two side transitions in `CH3OH_line8` and the reciprocal of variance, w

Plot of `CH3OH_line8` with Gaussian fit over center peak (look at those standard deviations!):
![plot_CH3OH_line8](https://user-images.githubusercontent.com/23585856/60352608-683c6780-9985-11e9-9a8e-bb69b318e875.png)

---|Peak 1 | Peak 2 | Peak 3
---|---|---|---
**Centroid (km/s)** | -4.66584 | 7.54641 | 64.2864
**Width (km/s)** | 2.63033 | 4.69701 | 8.2667 
**Rest Freq. (MHz)** | 24934.4010 | 24933.5040 | 24928.7280
**Offset (km/s)** | 10.8 | N/A | 57.5 
**w (s/km)^2** | 8.57e-3 | N/A | 3.02e-4

Equations
>Offset = (Δrest freq./side rest freq.) * c

>Reciprocal of variance, w = error^-2 

### Goals For Next Week

Calculate weighted arithmetic means of spectra centroids and widths

Find a way to tell `specfit()` to maintain new parameters 

Correct plot y-axes from Jy/beam to K using `radio_beam` package in PySpecKit 
