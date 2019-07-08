### Monday - 7/8

Methanol File | J Quantum Number
---|---
CH3OH_line8 P1 | 3
CH3OH_line8 P2 | 4
CH3OH_line8 P3 | 2
CH3OH_line10 | 5 
CH3OH_line11 | 6
CH3OH_line12 | 7
CH3OH_line13 | 8
CH3OH_line14 | 9
CH3OH_line15 | 10
CH3OH_line16 | 11

Plotted amplitudes of methanol data and J quantum numbers adding error bars:

```python
x = [2,3,4,5,6,7,8,9,10,11]
y = [4.94,3.39,4.58,5.11,3.60,4.89,4.58,4.86,3.81,4.18] #Rearranged from table to increase in J QNs
ampl_err = [0.64,0.55,0.56,0.34,0.41,0.46,0.32,0.54,0.43,0.61]

plt.plot(x,y,'o',color='black') 
plt.axis([0,12,0,5.50])
plt.errorbar(x,y,xerr=None,yerr=ampl_err,fmt='none',ecolor='blue')
plt.title('Methanol J Quantum Numbers vs. Amplitude')
plt.xlabel('Quantum Number')
plt.ylabel('Amplitude (mJ/bm)') 
```

![JQN_v_ampl](https://user-images.githubusercontent.com/23585856/60843140-110f7180-a193-11e9-9f83-e1f61427f7a6.png)

### Tuesday - 7/9

### Wednesday - 7/10

### Thursday - 7/11

### Friday - 7/12

### Goals For Next Week
