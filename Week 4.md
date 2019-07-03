N.B. Short week due to Independence Day

### Monday - 7/1

Read more of Krumholz's *Notes on Star Formation* review

Cleared up confusion surrounding the `CH3OH_line8` offsets, the weighted arithemetic means, and correcting the plot uncertainties

### Tuesday - 7/2

Calculated actual centroids of the side peaks in `CH3OH_line8` using the offsets:
> New centroid = old centroid - offset

> ---| Peak 1 | Peak 2 | Peak 3
> ---|---|---|---
> **Offset (km/s)** | -10.8 | N/A | 57.5 
> **Old Centroid (km/s)** | -4.66584 | 7.54641 | 64.2864
> **Centroid (km/s)** | 6.13416 | 7.54641 | 6.7864 

Must find a way to input minimum/maximum values for guesses in PySpecKit (possibly within `specfit()` or `Spectrum()`) that would correct for the absurdly large sigma values in original plots 

Found possible solution with `rms` and `minpars`/`maxpars` (example lacks necessary code):

```python
#rms = np.std(sp.data[])
rms = sqrt(sum(vals**2)/N)
sp.error[:] = rms

sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3], minpars=[4e-3,4,2], maxpars[8e-3,8,8]) 
```

Began reading A.G.G.M. Tielens' *The Molecular Universe* review

### Wednesday - 7/3

Used `rms` and adjusted `minpars`/`maxpars` to manually input parameters and changed `guesses` to fit actual amplitude/centroid/width values of data:

```python
import numpy as np
import pyspeckit as psk
from astropy import units as u
import pylab as pl
pl.ion()

sp.psk.Spectrum('CH3OH_line16_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=26313.093*u.MHz) 

rms = np.std(sp.data[0:50]) #Gives a range of channels without the peak to average the noise
sp.error[:] = rms
print(rms) #For future reference

sp.plotter(title='CH3OH_line16', xlabel='Radio Velocity (km/s)', ylabel='Jy / beam')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5]) 
```

Plot of `CH3OH_line16` with adjusted standard deviations:


Refit all methanol files:

```python
import numpy as np
import pyspeckit as psk
import math
from astropy import units as u
import pylab as pl
pl.ion()

sp = psk.Spectrum('CH3OH_line8_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24928.728*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line8', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[3e-3,0,0], maxpars=[10e-3,15,5]) 

sp = psk.Spectrum('CH3OH_line10_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=24959.123*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line10', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5]) 

sp = psk.Spectrum('CH3OH_line11_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25018.176*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line11', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])

sp = psk.Spectrum('CH3OH_line12_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25124.932*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line12', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])

sp = psk.Spectrum('CH3OH_line13_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25294.483*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line13', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])

sp = psk.Spectrum('CH3OH_line14_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25541.467*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line14', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])

sp = psk.Spectrum('CH3OH_line15_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=25878.239*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line15', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])

sp = psk.Spectrum('CH3OH_line16_B1.fits')
sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=26313.093*u.MHz) 
rms = np.std(sp.data[0:50])
sp.error[:] = rms
print(rms)
sp.plotter(title='CH3OH_line16', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,7,1], minpars=[0,0,0], maxpars=[1e-2,10,5])
```


Methanol File | RMS (J/bm) |  Amplitude (J/bm) | Amplitude σ (J/bm) | Centroid (km/s) | Centroid σ (km/s) | Width (km/s) | Width σ (km/s)
---|---|---|---|---
`CH3OH_line8` | 0.001226577966979845 | 4.58e-3 | 5.6e-4 | 6.91 | 0.11 | 0.77 | 0.11 
`CH3OH_line10` | 0.00067419757514329 | 5.11e-3 | 3.4e-4 | 6.804 | 0.049 | 0.641 | 0.049 
`CH3OH_line11` | 0.0009809577191390697 | 3.60e-3 | 4.1e-4 | 6.99 | 0.12 | 0.92 | 0.12 
`CH3OH_line12` | 0.0009926948354418738 | 4.89e-3 | 4.6e-4 | 6.85 | 0.08 | 0.73 | 0.08 
`CH3OH_line13` | 0.0007554915723677119 | 4.58e-3 | 3.2e-4 | 6.930 | 0.69 | 0.848 | 0.69 
`CH3OH_line14` | 0.001265012668199331 | 4.86e-3 | 5.4e-4 | 6.84 | 0.11 | 0.86 | 0.11
`CH3OH_line15` | 0.0010646074902382063 | 3.81e-3 | 4.3e-4 | 7.00 | 0.12 | 0.92 | 0.12
`CH3OH_line16` | 0.0011710828501256556 | 4.18e-3 | 6.1e-4 | 6.659 | 0.093 | 0.551 | 0.093 

N.B. There doesn't seem to be an apparent linear pattern to the RMS by methanol transition

Calculated weighted means for the data's centroid and width:

Weighted Arithmetic Mean = Σ(x * w)/Σ(w)

> Weighted Width =  

> Weighted Centroid = 


### Goals For Next Week

