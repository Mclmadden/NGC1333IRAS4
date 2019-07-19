### Monday - 7/15

Read K.M. Menten et al.'s *The Centimeter Transitions of E-type Methanol* article 

Read Paul F. Goldsmith and William D. Langer's *Population Diagram Analysis of Molecular Line Emission* article 

Messed around with the Overleaf template
> Tediously, added in all the tables

> Wrote in some equations for the body text 

Side note: Watched a broadcast of a workshop led by a Columbia astronomy grad student! \#RoarLionsRoar

### Tuesday - 7/16

Brian Svoboda realized the correct equation for calculating the radiation temperature:

Radiation temperature = antenna_temperature * 1/mean_value * (1+0.3^2)/0.3^2 

Which would also affect the output for the areas under the Gaussian curves:

Area = radiation_temperature * FWHM

(aperture_area^2 + source_area^2)/source_area^2 = (1+0.3^2)/(0.3^2) = 12.111 

Recalculated the radiation temperatures and areas:

Methanol File | Radiation Temperature (K) | Area Under the Curve (K.km/s) 
---|---|---
`CH3OH_line8` P3 | 34.5683 | 52.5898 
`CH3OH_line8` P2 | 34.5551 | 52.5697
`CH3OH_line8` P1 | 34.5526 | 52.5659 
`CH3OH_line10` | 36.6256 | 55.7197
`CH3OH_line11` | 36.7637 | 55.9297 
`CH3OH_line12` | 35.6886 | 54.2941 
`CH3OH_line13` | 36.6972 | 55.8286
`CH3OH_line14` | 33.3519 | 50.7392
`CH3OH_line15` | 35.7182 | 54.3392
`CH3OH_line16` | 36.7596 | 55.9234 

Opened `NGC1333IRAS4A_CH3OH_line8_m0p3.moment` in Inkscape to draw arrows and label each protostar:

![moment0_8P3](https://user-images.githubusercontent.com/23585856/61336086-32a0d680-a7ed-11e9-9a68-861c6bf9caae.png)

Continued to mess around with the Overleaf template 
> Wrote rough draft of abstract and some of the body text 

> Added various figures to potentially use in final paper

> Created the different sections of the body text: introduction, observations, methods, analysis, discussion, summary

> Added `NGC1333IRAS4A_CH3OH_line8_m0p3.moment` with labels 

### Wednesday - 7/17

No workday due to day-trip tours (including VLA and VLBA antennae climbs!)

### Thursday - 7/18

Awaiting technical details for Observation section of Overleaf report from Brian Svoboda

Worked on Overleaf report
> Wrote more for Introduction including references

> Wrote more for Methods and added equations for Rotation Diagram subsection 

Brian figured out how to calculate the fraction of column density over degeneracy (N_u/g_u) to bypass knowing the individual degeneracies and to fit the eventual rotation diagram with `numpy.polyfit`/`scipy.optimize...`(?)

### Friday - 7/19 

Read Karin I. Öberg et al.'s *Complex Molecules Toward Low-Mass Protostars: The Serpens Core* article 

Equation from Öberg et al. to find N_u/g_u:

(3k \int T_MB dV) / (8π^3 * ν * Sμ^2) = N_u/g_u
> k = Boltzmann's constant

> Integrated main-beam temperature = area under the Gaussian curve

> ν = transition rest frequency 

> Sμ^2 = line strength * dipole moment^2

> Sμ^2 found on Splatalogue as S_ij * μ^2 

Separated original Table 1 in Overleaf into Splatalogue info and fit info: 

Species | Rest Frequency (GHz) | J QN | E_l (K) | E_u (K) | S_ij * μ^2 (D^2)
---|---|---|---|---|---
CH3OH v_t=0-2 | 24.928728 | 3 | 34.97603 | 36.17285 | 11.22632
CH3OH v_t=0-2 | 24.933504 | 4 | 44.26285 | 45.45889 | 15.71141
CH3OH v_t=0-2 | 24.934401 | 2 | 28.01081 | 29.20804 | 6.37759
CH3OH v_t=0-2 | 24.959123 | 5 | 55.87113 | 57.06954 | 20.10152
CH3OH v_t=0-2 | 25.018176 | 6 | 69.80071 | 71.00110 | 24.51000
CH3OH v_t=0-2 | 25.124932 | 7 | 86.05160 | 87.25711 | 28.98505
CH3OH v_t=0-2 | 25.294483 | 8 | 104.62352 | 105.83687 | 33.55241
CH3OH v_t=0-2 | 25.541467 | 9 | 125.51616 | 126.74252 | 38.21532
CH3OH v_t=0-2 | 25.878239 | 10 | 148.72926 | 149.97179 | 42.95093
CH3OH v_t=0-2 | 26.313093 | 11 | 174.26265 | 175.52504 | 47.69542

RMS (J) | Amplitude (J) | Amplitude σ (J) | Centroid (km/s) | Width (km/s) | Centroid & Width σ (km/s) 
---|---|---|---|---|---
1.227 E-3 | 4.94 E-3 | 6.4 E-4 | 6.13 | 0.580 | 0.087 
1.227 E-3 | 4.58 E-3 | 5.6 E-4 | 6.91 | 0.77 | 0.11 
1.2267 E-3 | 3.39 E-3 | 5.5 E-4 | 6.79 | 0.80 | 0.15
0.674 E-3 | 5.11 E-3 | 3.4 E-4 | 6.80 | 0.641 | 0.049
0.981 E-3 | 3.60 E-3 | 4.1 E-4 | 6.99 | 0.92 | 0.12 
0.993 E-3 | 4.89 E-3 | 4.6 E-4 | 6.85 | 0.73 | 0.08 
0.755 E-3 | 4.58 E-3 | 3.2 E-4 | 6.93 | 0.848 | 0.69 
1.265 E-3 | 4.86 E-3 | 5.4 E-4 | 6.84 | 0.86 | 0.11 
1.065 E-3 | 3.81 E-3 | 4.3 E-4 | 7.00 | 0.92 | 0.12 
1.171 E-3 | 4.18 E-3 | 6.1 E-4 | 6.66 | 0.551 | 0.093 

Calculated each transition's natural log of N_u/g_u:

```python
import numpy as np 
from astropy import units as u
from astropy import constants as c
import math as mt
import matplotlib.pyplot as plt 
plt.ion()

#Function for calculating ln(N/g); input Gaussian area, rest frequency, S*mu^2
def lnNg(A,f,D):
    debye = 3.1623*10**(-25) * (u.J*u.m**3)**0.5
    Ng = (3 * c.k_B * A*u.K*u.km/u.s) / (8 * (mt.pi**3) * f*u.GHz * D*debye**2)
    uNg = Ng.to('cm**-2')
    yaxis = mt.log(uNg.value) * u.cm**-2
    print(yaxis)

lnNg(52.5898,24.928728,11.22632)
lnNg(52.5697,24.933504,15.71141)
lnNg(52.5659,24.93401,6.37759)
lnNg(55.7197,24.959123,20.10152)
lnNg(55.9297,24.018176,24.51)
lnNg(54.2941,25.124932,28.98505)
lnNg(55.8286,25.294483,33.55241)
lnNg(50.7392,25.5414567,38.21532)
lnNg(54.3392,25.878239,42.95093)
lnNg(55.9234,26.313093,47.69542)
```

### Goals For Next Week
