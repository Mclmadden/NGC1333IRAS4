N.B. Short week due to Independence Day

### Monday - 7/1

Read more of Krumholz's *Notes on Star Formation* review

Cleared up confusion surrounding the `CH3OH_line8` offsets, the weighted arithemetic means, and correcting the plot uncertainties

### Tuesday - 7/2

Calculated actual centroids of the side peaks in `CH3OH_line8` using the offsets:
> New centroid = old centroid - offset

> ---| Peak 1 | Peak 2 | Peak 3
> ---|---|---|---
> **Offset (km/s)** | -10.8 | N/A | 57.5 
> **Old Centroid (km/s)** | -4.66584 | 7.54641 | 64.2864
> **Centroid (km/s)** | 6.13416 | 7.54641 | 6.7864 

Must find a way to input minimum/maximum values for guesses in PySpecKit (possibly within `specfit()` or `Spectrum()`) that would correct for the absurdly large sigma values in original plots 

Found possible solution with `rms` and `minpars`/`maxpars`:

```python
sp = psk.Spectrum('CH3OH_line16_B1.fits')

#rms = np.std(sp.data[])
rms = sqrt(sum(vals**2)/N)
sp.error[:] = rms

sp.xarr.convert_to_unit(u.MHz)
sp.xarr.convert_to_unit(u.km/u.s, rest_value=26313.093*u.MHz)

sp.plotter(title='CH3OH_line16', xlabel='Radio Velocity (km/s)', ylabel='Intensity (Jy/bm)')
sp.specfit(fittype='gaussian', guesses=[5.5e-3,5,3], minpars=[4e-3,4,2], maxpars[8e-3,8,8]) 
```

Began reading A.G.G.M. Tielens' *The Molecular Universe* review

### Wednesday - 7/3



### Goals For Next Week
