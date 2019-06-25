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

Used PySpecKit to fit a Gaussian to spectrum of `CH3OH_line8` at protostar B1: 

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u

sp = psk.Spectrum('CH3OH_line8_B1.fits') #Reads FITS file into PySpecKit
sp.plotter()

#Fit with input guesses 
amplitude_guess = 5.5 * u.mJy/u.beam
center_guess = 6.5 * u.km/u.s
width_guess = 3 * u.km/u.s
guesses = [amplitude_guess, center_guess, width_guess]

sp.specfit(fittype='gaussian', guesses=guesses)
```

### Wednesday - 6/26/19
