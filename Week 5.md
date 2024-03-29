### Monday - 7/8

Methanol File | J Quantum Number
---|---
`CH3OH_line8` P1 | 2
`CH3OH_line8` P2 | 4
`CH3OH_line8` P3 | 3
`CH3OH_line10` | 5 
`CH3OH_line11` | 6
`CH3OH_line12` | 7
`CH3OH_line13` | 8
`CH3OH_line14` | 9
`CH3OH_line15` | 10
`CH3OH_line16` | 11

Plotted methanol transition J quantum numbers vs. amplitudes, including error bars:

```python
import matplotlib.pyplot as plt
plt.ion()

#Rearrange y and ampl_err so that JQNs are in increasing order
x = [2,3,4,5,6,7,8,9,10,11]
y = [4.94,3.39,4.58,5.11,3.60,4.89,4.58,4.86,3.81,4.18] 
ampl_err = [0.64,0.55,0.56,0.34,0.41,0.46,0.32,0.54,0.43,0.61]

plt.plot(x,y,'o',color='black') 
plt.axis([0,12,0,6])
plt.errorbar(x,y,xerr=None,yerr=ampl_err,fmt='none',ecolor='blue')
plt.title('CH3OH J Quantum Numbers vs. Amplitude')
plt.xlabel('J Quantum Number')
plt.ylabel('Amplitude (mJ/bm)') 
```

![JQN_ampl](https://user-images.githubusercontent.com/23585856/61477527-ba512700-a94c-11e9-9f16-7a83f1b4b759.png)

Read more of Tielens' *The Molecular Universe* review

### Tuesday - 7/9

Read more of Tielens' *The Molecular Universe* review

Upper and lower energy levels of methanol transitions according to SLAIM data on Splatalogue:

Methanol File | Energy of Upper Level (K) | Energy of Lower Limit (K) 
---|---|---
`CH3OH_line8` P1 | 29.20804 | 28.01139
`CH3OH_line8` P2 | 45.45889 | 44.26228
`CH3OH_line8` P3 | 36.17285 | 34.97647
`CH3OH_line10` | 57.06954 | 55.87170
`CH3OH_line11` | 71.00110 | 69.80042
`CH3OH_line12` | 87.25711 | 86.05131
`CH3OH_line13` | 105.83687 | 104.62294
`CH3OH_line14` | 126.74252 | 125.51674
`CH3OH_line15` | 149.97179 | 148.72983
`CH3OH_line16` | 175.52504 | 174.26222 

Learned the proper axes units for a rotation diagram  
> x-axis: energy of upper limit divided by Boltzman's constant, Eu/k (Kelvin)

> y-axis: natural log of column density of upper limit over g of upper limit, ln(Nu/gu) (cm^-2)

### Wednesday - 7/10

Changed x-axis of methanol plot to Energy of Upper Level (K):

```python
import matplotlib.pyplot as plt
plt.ion()

x = [29.21,36.17,45.46,57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [4.94,3.39,4.58,5.11,3.60,4.89,4.58,4.86,3.81,4.18] 
ampl_err = [0.64,0.55,0.56,0.34,0.41,0.46,0.32,0.54,0.43,0.61]

plt.plot(x,y,'o',color='black') 
plt.axis([0,180,0,6])
plt.errorbar(x,y,xerr=None,yerr=ampl_err,fmt='none',ecolor='blue')
plt.title('CH3OH Energy of Upper Level vs. Amplitude')
plt.xlabel('$E_U$ (K)')
plt.ylabel('Amplitude (mJ/bm)')
```

![EU_ampl](https://user-images.githubusercontent.com/23585856/61002076-11884380-a31e-11e9-9320-7b7856128f17.png)

Used CASA's `imhead` and `header` tasks to get beam sizes for methanol files

Example using `CH3OH_line8`:

```python
casa #will not run if CASA isn't installed
header = imhead('NHC1333IRAS4A_CH3OH_line8.image',mode='summary')
header['perplanebeams']['beams']['*0']['*0']['major']['value']
```

Used CASA Viewer to get mean values of regions in psf files 

Used PySpecKit's `radio_beam` package to convert y-axis from amplitude (mJ/bm) to radiation temperature (K), and multiplied radiation temperature by each transition's width to get the area under the Gaussian curve:

```python
from radio_beam import Beam
from astropy import units as u

b8_3 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_3,24.928728*u.GHz)) #Uses rest frequency 
rtemp = atemp*(1/0.6879)*((1/0.3)**2) #Multiply by max_peak/mean_value and (aperture_area/source_area)^2
print(rtemp)

b8_2 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_2,24.933504*u.GHz))
rtemp = atemp*(1/0.6879)*((1/0.3)**2)
print(rtemp)

b8_1 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_1,24.934401*u.GHz))
rtemp = atemp*(1/0.6879)*((1/0.3)**2)
print(rtemp)

b10 = Beam(0.9697425365447998*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b10,24.9959123*u.GHz))
rtemp = atemp*(1/0.6878)*((1/0.3)**2)
print(rtemp)

b11 = Beam(0.9680445194244385*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b11,25.018176*u.GHz))
rtemp = atemp*(1/0.6864)*((1/0.3)**2)
print(rtemp)

b12 = Beam(0.9767780900001526*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b12,25.124932*u.GHz))
rtemp = atemp*(1/0.6886)*((1/0.3)**2)
print(rtemp)

b13 = Beam(0.9611411094665527*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b13,25.294483*u.GHz))
rtemp = atemp*(1/0.6824)*((1/0.3)**2)
print(rtemp)

b14 = Beam(1.0004248467414423*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b14,25.541467*u.GHz))
rtemp = atemp*(1/0.6797)*((1/0.3)**2)
print(rtemp)

b15 = Beam(0.9594455361366272*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b15,25.878239*u.GHz))
rtemp = atemp*(1/0.6722)*((1/0.3)**2)
print(rtemp)

b16 = Beam(0.9355015754699707*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b16,26.313093*u.GHz))
rtemp = atemp*(1/0.6645)*((1/0.3)**2)
print(rtemp)
```
### Thursday - 7/11

N.B. Shortened work day because of EMRTC tour!

Calculated full width at half maximum (FWHM) to calculate the areas under the Gaussian curves:
> FWHM (km/s) = 2.355 * weighted width = 2.355 * 0.646 = 1.521 km/s 

> Area (K.km/s) = FWHM * radiation_temperature 

Methanol File | Beam Size (arcsec) | Mean Value (unitless) | Radiation Temperature (K) | Area Under Curve (K.km/s)  
---|---|---|---|---
`CH3OH_line8` P3 | 1.0007993958627737 | 0.6879 | 31.7141 | 48.2476
`CH3OH_line8` P2 | " | " | 31.7019| 48.2291
`CH3OH_line8` P1 | " | " | 31.6996 | 48.2256
`CH3OH_line10` | 0.9697425365447998 | 0.6878 | 33.6015 | 51.1190
`CH3OH_line11` | 0.9680445194244385 | 0.6864 | 33.7281 | 51.3116
`CH3OH_line12` | 0.9767780900001526 | 0.6886 | 32.7418 | 49.8111
`CH3OH_line13` | 0.9611411094665527 | 0.6824 | 33.6672 | 51.2189
`CH3OH_line14` | 1.0004248467414423 | 0.6797 | 30.5980 | 46.5497
`CH3OH_line15` | 0.9594455361366272 | 0.6722 | 32.7690 | 49.8524
`CH3OH_line16` | 0.9355015754699707 | 0.6645 | 33.7244 | 51.3059

### Friday - 7/12

Awaiting the calculations of degeneracy values, g, required for rotation diagram

Read Jeffrey G. Mangum and Yancy L. Shirley's *How to Calculate Molecular Column Density* article 

### Goals For Next Week

Obtain column densities and degeneracy values

Create rotation diagram and fit a line 

Calculate total excitation temperature from slope of rotation diagram

Analyze findings and begin paper on Overleaf
