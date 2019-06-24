### Monday - 6/24/19

Made moment map of `CH3OH_line8` FITS file:

```python
cd /lustre/aoc/students/mmadden/downlaods/NGC1333IRAS4A
casa #will not run if CASA isn't installed

default('immoments')
imagename = 'NGC1333IRAS4A_CH3OH_line8.fits'
moments=[0,1]
axis='spectral'
chans='1~5'
includepix=[4,100]
outfile='NGC1333IRAS4A_CH3OH_line8'
```
