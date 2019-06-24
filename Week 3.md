### Monday - 6/24/19

Made moment map of `CH3OH_line8` FITS file:

```python
import astropy.units as u
from astropy.utils import data
from spectral_cube import SpectralCube

#Read in FITS file
cube = SpectralCube.read('NGC1333IRAS4A_CH3OH_lin8.fits')

moment_0 = cube.moment(order=0)
moment_1 = cube.moment(order=1)
moment_2 = cube.moment(order =2)
```
