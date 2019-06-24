### Monday - 6/24/19

Made moment map of `CH3OH_line8` FITS file:

```python
import astropy.units as u
from astropy.utils import data
from spectral_cube import SpectralCube

#Read in FITS file
cube = SpectralCube.read('NGC1333IRAS4A_CH3OH_lin8.fits')

slab_1 = cube.spectral_slab(50 *u.km/u.s, 75 *u.km/u.s)

moment_0 = slab_1.moment(order=0)
moment_0.write('CH3OH_line8_1.fits', overwrite=True)

```
