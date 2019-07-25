### Monday - 7/22

Used `numpy.polyfit()` to obatin parameters for rotation diagram line of best fit
> Calculated the weight values: (widths * amplitude σ)^-1 

> `np.polyfit(x,y,degree,full=boolean,w=[array])`

> Return of polynomial coefficients in the format of array[m,b] where m = slope and b = y-intercept

```python
import numpy as np

#Fourth through tenth data points
weight = [3.4e-4*0.641,4.1e-4*0.92,4.6e-4*0.73,3.2e-4*0.848,
          5.4e-4*0.86,4.3e-4*0.92,6.1e-4*0.551]
one = 1
w = [one/x for x in weight]
x = [57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [30.551180703326107,30.395085249636868,30.15265650494573,30.027473059502565,
     29.792041199312983,29.730666937248277,29.637962651957622]
np.polyfit(x,y,1,full=True,w=w)

# First three data points
weight = [6.4e-4*0.580, 5.6e-4*0.77, 5.5e-4*0.80]
w = [one/x for x in weight]
x = [29.21,36.17,45.46]
y = [31.641926381766012,31.07712206910506,30.740422046193565] 
np.polyfit(x,y,1,full=True,w=w)
```

Returned:
> Polynomial coefficients: array([-8.10619096e-03, 30.9523523]) and array([-0.05564832, 33.21459443])

> Residuals of least-squares fit: array([404647.06224484]) and array([119811.22201457])

> Effective rank of the scaled Vandermonde coefficient matrix: 2 and 2

> Singular values of the sVc matrix: array([1.38773859, 0.27236303]) and array([1.40825687, 0.12966338])

> Specified value of *rcond*: 1.5543122344752192e-15 and 6.661338147750939e-16 

Used polynomial coefficients to calculate T_rot for both sections 
> T_rot = m^-1

> T_rot7 = (-8.10619096e-03)^-1 = 123.36250218314619

> T_rot3 = (-0.05564832)^-1 = 17.969994422113732

Used ranges of T_rot on Splatalogue (CDMS) to calculate rotation partition function, Q(T_rot)
> T_rot7 fell between Q(75)=2924.3023 and Q(150)=9750.0398

> T_rot3 fell between Q(9.375)=78.1735 and Q(18.75)=274.9880 

Used y=mx+b form to fit two lines to the two sections of data:

```python
import numpy as np
import matplotlib.pyplot as plt
plt.ion()

x = [29.21,36.17,45.46,57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [31.641926381766012,31.07712206910506,30.740422046193565,30.551180703326107,
     30.395085249636868,30.15265650494573,30.027473059502565,29.792041199312983,
     29.730666937248277,29.637962651957622]

plt.plot(x,y,'o',color='black')
plt.axis([0,200, 29,33.5])

space3 = np.linspace(0,100,50)
line3 = -0.05564832*space3 + 33.21459443
plt.plot(space3,line3,'--r',label='y = 33.21459443 - 0.05564832x')

space7 = np.linspace(0,200,100)
line7 = -8.10619096e-03*space7 + 30.9523523
plt.plot(space7,line7,'--b',label='y = 30.9523523 - 8.10619096e-03x')

plt.legend(loc='upper right')
plt.title('CH3OH Rotation Diagram')
plt.xlabel('$E_u/k$ (K)')
plt.ylabel('ln($N_u$/$g_u$) (cm$^{-2}$)')
```

![rot_diagram_lines](https://user-images.githubusercontent.com/23585856/61669706-3aa1c000-ac9e-11e9-9647-705f7739c4c0.png)

Worked on Overleaf report 

### Tuesday - 7/23

Calculated rotation partition functions, Q(T_rot), using linear interpolation (`scipy.interpolate.interp1d` and by hand) 

Splatalogue info:

Rotation Temperature (K) | Rotation Partition Function
---|---
9.375 | 78.1735
18.75 | 274.9880
37.50 | 920.9637
75.00 | 2924.3023
150.0 | 9750.0398
225.0 | 20991.8100
300.0 | 37027.3292
500.0 | 102146.4089
1000 | 347799.0417

```python
import scipy as sp
from scipy import interpolate

T = [9.375,18.75,37.5,75,150,225,300,500,1000]
Q = [78.1735,274.988,920.9637,2924.3023,9750.0398,20991.81,37027.3292,102146.4089,347799.0417]

f = sp.interpolate.interp1d(T,Q)

cold = 17.97
hot = 123.3625

print(f(cold), f(hot))
```

Calculated Q(17.97) = 258.6130336 and Q(123.3625) = 7325.765364583334 using Scipy

Calculated Q(17.97) = 258.6130336 and Q(123.3625) = 7325.765365 by hand and proved to be accurate (eugepae!)

```python
import math as mt

Ncold = 258.6130336 * mt.exp(33.21459443)
Nhot = 7325.765364583334 * mt.exp(30.9523523)
print(Ncold)
print(Nhot)
```

Calculated N_T = 6.87964E+16 cm^-2 and N_T 2.02903E+17 cm^-2 utilizing the y-intercept (b) and ln(N_T/Q(T_rot))

Worked on Overleaf report 

### Wednesday - 7/24 

From Brian Svoboda: 
> Cold / (Cold + Hot)

> 6.87964E+16 / (6.87964E+16 + 2.02903E+17) = 0.253207773

> Only ~25% of the total molecular column density is in the cold component 

Talked to Claire Chandler about results
> Once error bars are added to rotation diagram, check if the 2 lines are good approximations for cold and hot components

> Compare curve with standard N and T profiles (as functions of radius from the protostar) 

> Emailed VLA observing proposal and an article on measuring distance to NGC 1333

> Data points closer to the protostar are unresolved with a resolution ~1 arcsec.

> If any results depend on distance, calculate distance in pc, but leave distance as variable in an equation to allow for future corrections 

> Moment map: second "blob" of methanol detection next to B1 could be real because of the system's water maser 

> MM: light free-free emission seen in countour map around A1 indicates direction of its outflow 

> MM: large methanol outflow most likely from A2  

Worked on Overleaf report 

### Thursday - 7/25

Calculated error bars for rotation diagram's amplitude:

Error = ampl. σ / ampl.

```
import matplotlib.pyplot as plt
plt.ion()

x = [29.21,36.17,45.46,57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [31.641926381766012,31.07712206910506,30.740422046193565,30.551180703326107,
     30.395085249636868,30.15265650494573,30.027473059502565,29.792041199312983,
     29.730666937248277,29.637962651957622]
     
p3 = (6.4E-4)/(4.94E-3)
p2 = (5.6E-4)/(4.58E-3)
p1 = (5.5E-4)/(3.39E-3)
l10 = (3.4E-4)/(5.11E-3)
l11 = (4.1E-4)/(3.6E-3)
l12 = (4.6E-4)/(4.89E-3)
l13 = (3.2E-4)/(4.58E-3)
l14 = (5.4E-4)/(4.86E-3)
l15 = (4.3E-4)/(3.81E-3)
l16 = (6.1E-4)/(4.18E-3)
ampl_err = [p3,p2,p1,l10,l11,l12,l13,l14,l15,l16]


plt.errorbar(x,y,xerr=None,yerr=ampl_err,fmt='none',ecolor='black')
plt.plot(x,y,'o',markersize=4,color='black')
plt.axis([0,200, 29,33.5])

space3 = np.linspace(0,100,50)
line3 = -0.05564832*space3 + 33.21459443
plt.plot(space3,line3,'--r',label='y = 33.21459443 - 0.05564832x')

space7 = np.linspace(0,200,100)
line7 = -8.10619096e-03*space7 + 30.9523523
plt.plot(space7,line7,'--b',label='y = 30.9523523 - 8.10619096e-03x')

plt.legend(loc='upper right')
plt.title('CH$_3$OH Rotation Diagram')
plt.xlabel('$E_u/k$ (K)')
plt.ylabel('ln($N_u$/$g_u$) (cm$^{-2}$)')
```

![rot_diagram_lines_err](https://user-images.githubusercontent.com/23585856/61890267-5686ab00-aec4-11e9-9acd-7058e8757485.png)

### Friday - 7/26



### Goals For Next Week 

