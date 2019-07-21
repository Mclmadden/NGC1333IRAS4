### Monday - 7/22

Used `numpy.polyfit()` to obatin parameters for rotation diagram line of best fit
> Calculated the weight values: (widths * amplitude σ)^-1 

> `np.polyfit(x,y,degree,full=boolean,w=[array])`

```python
import numpy as np

x = [29.21,36.17,45.46,57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [31.641926381766012,31.07712206910506,30.740422046193565,30.551180703326107,
     30.395085249636868,30.15265650494573,30.027473059502565,29.792041199312983,
     29.730666937248277,29.637962651957622]
weight = [6.4e-4*0.580,5.6e-4*0.77,5.5e-4*0.80,3.4e-4*0.641,4.1e-4*0.92,4.6e-4*0.73,
          3.2e-4*0.848,5.4e-4*0.86,4.3e-4*0.92,6.1e-4*0.551]
w = weight**-1

np.polyfit(x,y,1,full=True,w=w)
```

### Tuesday - 7/23



### Wednesday - 7/24 



### Thursday - 7/25



### Friday - 7/26



### Goals For Next Week 

