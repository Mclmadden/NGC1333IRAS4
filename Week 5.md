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
y = [3.39,4.94,4.58,5.11,3.60,4.89,4.58,4.86,3.81,4.18] 
ampl_err = [0.55,0.64,0.56,0.34,0.41,0.46,0.32,0.54,0.43,0.61]

plt.plot(x,y,'o',color='black') 
plt.axis([0,12,0,6])
plt.errorbar(x,y,xerr=None,yerr=ampl_err,fmt='none',ecolor='blue')
plt.title('CH3OH J Quantum Numbers vs. Amplitude')
plt.xlabel('J Quantum Number')
plt.ylabel('Amplitude (mJ/bm)') 
```

![JQN_ampl](https://user-images.githubusercontent.com/23585856/60921396-9c523b00-a257-11e9-8a5f-5ffae3854f50.png)

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

Used PySpecKit's `radio_beam` package to convert y-axis from amplitude (mJ/bm) to radiative temperature (K), and multiplied radiative temperature by each transition's width to get the area under the Gaussian curve:

```python
from radio_beam import Beam
from astropy import units as u

b8_3 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_3,24.928728*u.GHz)) #Uses rest frequency 
rtemp = atemp*(1/0.3)*(1/0.6879) #Multiply by aperture_area/source_area and max_peak/mean_value
print(rtemp)

b8_2 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_2,24.933504*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6879)
print(rtemp)

b8_1 = Beam(1.0007993958627737*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b8_1,24.934401*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6879)
print(rtemp)

b10 = Beam(0.9697425365447998*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b10,24.9959123*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6878)
print(rtemp)

b11 = Beam(0.9680445194244385*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b11,25.018176*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6864)
print(rtemp)

b12 = Beam(0.9767780900001526*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b12,25.124932*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6886)
print(rtemp)

b13 = Beam(0.9611411094665527*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b13,25.294483*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6824)
print(rtemp)

b14 = Beam(1.0004248467414423*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b14,25.541467*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6797)
print(rtemp)

b15 = Beam(0.9594455361366272*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b15,25.878239*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6722)
print(rtemp)

b16 = Beam(0.9355015754699707*u.arcsec)
atemp = (1*u.mJy).to(u.K, u.brightness_temperature(b16,26.313093*u.GHz))
rtemp = atemp*(1/0.3)*(1/0.6645) 
print(rtemp)
```
### Thursday - 7/11

N.B. Shortened work day because of EMRTC tour!

Calculated full width at half maximum (FWHM) to find area under the Gaussian curves:
> FWHM (km/s) = 2.355 * width 

> Area (K.km/s) = FWHM * radiative temperature 

Methanol File | Beam Size (arcsec) | Mean Value (unitless) | Radiative Temperature (K) | Width (km/s) | FWHM (km/s) | Area Under Curve (K.km/s)  
---|---|---|---|---|---|---
`CH3OH_line8` P3 | 1.0007993958627737 | 0.6879 | 9.5142 | 0.58 | 1.37 | 13.00 
`CH3OH_line8` P2 | " | " | 9.5106 | 0.77 | 1.81 | 17.2460 
`CH3OH_line8` P1 | " | " | 9.5099 | 0.80 | 1.88 | 17.9166
`CH3OH_line10` | 0.9697425365447998 | 0.6878 | 10.0804 | 0.641 | 1.51 | 15.22
`CH3OH_line11` | 0.9680445194244385 | 0.6864 | 10.1184 | 0.92 | 2.17 | 21.92 
`CH3OH_line12` | 0.9767780900001526 | 0.6886 | 9.8225 | 0.73 | 1.72 | 16.89
`CH3OH_line13` | 0.9611411094665527 | 0.6824 | 10.1002 | 0.848 | 2.00 | 20.17
`CH3OH_line14` | 1.0004248467414423 | 0.6797 | 9.1794 | 0.86 | 2.03 | 18.59 
`CH3OH_line15` | 0.9594455361366272 | 0.6722 | 9.8307 | 0.92 | 2.17 | 21.30
`CH3OH_line16` | 0.9355015754699707 | 0.6645 | 10.1173 | 0.551 | 1.30 | 13.13

### Friday - 7/12


### Goals For Next Week

