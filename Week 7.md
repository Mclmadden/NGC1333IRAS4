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

Used ranges of T_rot on Splatalogue to calculate rotation partition function, Q(T_rot)
> T_rot7 fell between Q(75)=2924.3023 and Q(150)=9750.0398

> T_rot3 fell between Q(9.375)=78.1735 and Q(18.75)=274.9880 

Used y=mx+b form to fit two lines to the two sections of data:

```python
x = [29.21,36.17,45.46,57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [31.641926381766012,31.07712206910506,30.740422046193565,30.551180703326107,
     30.395085249636868,30.15265650494573,30.027473059502565,29.792041199312983,
     29.730666937248277,29.637962651957622]

plt.plot(x,y,'o',color='black')
plt.axis([0,200, 28,32])

plt.title('CH3OH Rotation Diagram')
plt.xlabel('$E_u/k$ (K)')
plt.ylabel('ln($N_u$/$g_u$) (cm$^-2$)')

space3 = np.linspace(20,48,50)
line3 = -0.05564832*space3 + 33.21459443
plt.plot(space3,line3,'--r',label='y = 33.21459443 - 0.05564832x')

space7 = np.linspace(49,200,100)
line7 = -8.10619096e-03*space7 + 30.9523523
plt.plot(space7,line7,'--b',label='y = 30.9523523 - 8.10619096e-03x')

plt.legend(loc='upper right')
```

![rotation_diagram_fitted](https://user-images.githubusercontent.com/23585856/61667794-3377b380-ac98-11e9-8e34-e5d6f34c01ae.png)

Worked on Overleaf report 

### Tuesday - 7/23



### Wednesday - 7/24 



### Thursday - 7/25



### Friday - 7/26



### Goals For Next Week 

