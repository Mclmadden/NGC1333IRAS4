### Monday - 6/17/19

Received two reduced data files: `CH3OH_line8`, which are the lowest three 2 --> 1 methanol lines, and `NH3_33`, which is the ammonia (3,3) inversion transition 

Received non-reduced file: `NGC1333IRAS4A_contful_p0`, which is the 1.4 cm wavelength continuum 

Learned the basics of CASA Viewer, such as adding regions to take spectra diagrams and making P/V diagrams 

### Tuesday - 6/18/19

Used CASA's `impbcor` (primary beam correction) command to reduce the 1.4 cm wavelength continuum image:

```python
casa #will not run if CASA isn't installed
impbcor(imagename='NGC1333IRAS4A_contful_p0.image.tt0', pbimage='MGC1333IRAS4A_contful_p0.pb.tt0', outfile='NGC1333IRAS4A _contful_p0.pbcor')
```

### Wednesday - 6/19/19

Used CASA Viewer to overlay contour map of reduced continuum with rastor images of `CH3OH_line8` and `NH3_33`

Checked for detection of `CH3OH_line8` and `NH3_33` toward A1, A2, B1, B2, and C protostars

Started Google Sheet "NGC1333IRAS4 Spectra" to record positive and negative detections of `CH3OH_line8` and `NH_33`

Received remaining methanol and ammonia data reduced by Brian Svoboda 

**Q-Branch Transitions of Methanol Data:**

Rest Frequency (MHz) |---|--------------| Upper Level Energy (K)|---| Quantum Numbers | Upper Symmetry State (J, Ka, Kc, s) | Lower Symmetry State (J, Ka, Kc, s) |---
---|---|---|---|---|---|---|---|---
  24928.7280  | 0.013  |  -5.9530 3  | 24.3097 | 28 | 325041404 | 3(2,2) 1 |   3(1,2) 1    |    CH3OH, vt=0-2
  24933.5040  | 0.012  |  -5.8203 3  | 30.7644 | 36 | 325041404 | 4(2,3) 1 |   4(1,3) 1    |    CH3OH, vt=0-2
  24934.4010  | 0.013  |  -6.1883 3  | 19.4686 | 20 | 325041404 | 2(2,1) 1 |   2(1,1) 1    |    CH3OH, vt=0-2
  24959.1230  | 0.012  |  -5.7292 3  | 38.8326 | 44 | 325041404 | 5(2,4) 1 |   5(1,4) 1    |    CH3OH, vt=0-2
  25018.1760  | 0.012  |  -5.6612 3  | 48.5142 | 52 | 325041404 | 6(2,5) 1 |   6(1,5) 1    |    CH3OH, vt=0-2
  25124.9320  | 0.012  |  -5.6082 3  | 59.8092 | 60 | 325041404 | 7(2,6) 1 |   7(1,6) 1    |    CH3OH, vt=0-2
  25294.4830  | 0.013  |  -5.5657 3  | 72.7174 | 68 | 325041404 | 8(2,7) 1 |   8(1,7) 1    |    CH3OH, vt=0-2
  25541.4670  | 0.014  |  -5.5310 3  | 87.2386 | 76 | 325041404 | 9(2,8) 1 |   9(1,8) 1    |    CH3OH, vt=0-2

### Thursday - 6/20/19

Completed Google Sheet "NGC1333IRAS4 Spectra" with recordings of positive and negative detections of remaining methanol and ammonia transitions

**Methanol Files:** `CH3OH_line8`, `CH3OH_line10`, `CH3OH_line11`, `CH3OH_line12`, `CH3OH_line13`, `CH3OH_line14`, `CH3OH_line15`, `CH3OH_line16`

All methanol transitions were detected toward A1, A2, and B1. 
No transitions detected toward B2 and C. 

N.B. Because `CH3OH_line8` contains three transitions, its spectrum shows three different peaks.

**Ammonia Files:** `NH3_11`, `NH3_22`, `NH3_33`, `NH3_44`, `NH3_55`, `NH3_66`, `NH3_77`

All ammonia transitions were detected toward A1, A2, and B1. 
Only `NH3_11` was detected toward B2. 
No transitions were detected toward C.

### Friday 6/21/19

**Regions/aperture drawn over contour map at protostar locations:**

------------------------------|A1|A2|B1|B2|C
---|---|---|---|---|---
**Center X (hr:min:sec of arc)**   |  3:29:10.539  |   3:29:10.435  |  3:29:12.018 |  3:29:12.841  | 3:29:12.551
**Center Y (deg., arcmin, arcsec)**| 31, 13, 30.886| 31, 13, 32.096 | 31, 13, 7.975| 31, 13, 6.854 | 21, 13, 58.143

N.B. The beam, width x height = 1x1 arcsecond for all regions

Saved spectra of each methanol and ammonia transition at protostars A1, A2, and B1 (with the exception of `NH3_11` spectra taken at protostars B2 and C in addition) as FITS files in directory `NGC1333IRAS4_Spectra` under `Spectra_NH3` and `Spectra_CH3OH` respectively. `NH3_11` shows a positive detection toward protostar B2; `NH3_11` also appears to have an absorption line(?) in its spectrum at protostar C. 

Used CASA's `exportfits` command to convert `CH3OH_line8` from an image to a FITS file:

```python 
casa #will not run if CASA isn't installed
exportfits(imagename='NGC1333IRAS4A_CH3OH_line8.image', fitsimage='NGC1333IRAS4A_CH3OH_line8.fits')
```

### Goals For Next Week

Make a moment map from `CH3OH_line8` FITS file

Plot methanol spectra in python

Average out all methanol spectra to make super spectra
