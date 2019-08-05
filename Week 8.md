### Monday - 7/29

Worked on ppt presentation

Worked on Overleaf report

### Tuesday - 7/30

Met with Brian Svoboda to add uncertainty values to T_ex by including covariance in `numpy.polyfit()`:

```python
import numpy as np

one = 1

weight = [3.4e-4*0.641,4.1e-4*0.92,4.6e-4*0.73,3.2e-4*0.848,
          5.4e-4*0.86,4.3e-4*0.92,6.1e-4*0.551]
w = [one/x for x in weight]
x = [57.07,71.00,87.26,105.84,126.74,149.97,175.53]
y = [30.551180703326107,30.395085249636868,30.15265650494573,30.027473059502565,
     29.792041199312983,29.730666937248277,29.637962651957622]
np.polyfit(x,y,w=w,cov=True)

weight = [6.4e-4*0.580, 5.6e-4*0.77, 5.5e-4*0.80]
w = [one/x for x in weight]
x = [29.21,36.17,45.46]
y = [31.641926381766012,31.07712206910506,30.740422046193565] 
np.polyfit(x,y,w=w,cov=True)
```

Worked on ppt presentation

Worked on Overleaf report

### Wednesday - 7/31 

Uncertainty values looked off, ignore for the time being

Worked on ppt presentation

Worked on Overleaf report

### Thursday - 8/1

Rehearsed ppt presentation with Brian Svoboda

Worked on Overleaf report

### Friday - 8/2 

Ppt presentation!

Presentation from coworker too

Worked on Overleaf report

### Goals For Next Week

Finish Overleaf report 
