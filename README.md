# Free-fall
Free fall 
# -*- coding: utf-8 -*-
"""
Created on Fri Sep 25 16:51:08 2026

@author: bas el patron 
"""
## luuk, brayan, bas, mathias 

"Movement upwards is positive speed"
import matplotlib.pyplot as plt
import math
while True:
    try:
        v = v_noair = v_init = float(input("Enter initial speed (m/s): "))
    except ValueError:
            print("Please enter a number:")
            continue
    if type(v) == float and v > 0 :
        break
    else:
        print("Please enter a positive value")
        continue
h = 0
h_noair = 0
t = 0
t_noair = 0
while True:
    try:
        m = float(input("Enter mass (kg): "))
    except ValueError:
        print("Please enter a number:")
        continue
    if type(m) == float and m > 0 :
        break
    else:
        print("Please enter a positive value")
        continue
g = -9.81
dt = 0.001
p = 1.225
C = 0.47

while True:
    try:
        r = float(input("Enter radius of ball (meters): "))
    except ValueError:
        print("Please enter a number:")
        continue
    if type(r) == float and r > 0 :
        break
    else:
        print("Please enter a positive value")
        continue

c = 0.5*p*math.pi*r**2
speeds_air= [v]
heights_air = [h]
times_air = [t]
speeds_noair = [v]
heights_noair = [h]
times_noair = [t]

def f(v):
    return (c*v**2)/m
while h >= 0:
    if v >= 0:
        dvdt = g - f(v)
    elif v < 0:
        dvdt = g + f(v)
    v += dvdt*dt
    h += v*dt
    t += dt
    speeds_air.append(v)
    heights_air.append(h)
    times_air.append(t)
while h_noair >= 0:
    dvdt = g
    v_noair += dvdt*dt
    h_noair += v_noair*dt
    t_noair += dt
    speeds_noair.append(v_noair)
    heights_noair.append(h_noair)
    times_noair.append(t_noair)
    
fig, ax = plt.subplots()
""""ax.plot(times, speeds, color = "black")"""
ax.plot(times_air, heights_air, color = "blue", label = "With air res.")
ax.plot(times_noair, heights_noair, color = "red", label = "Without air res.")
ax.set_xlabel("Time in s")
ax.set_ylabel("Height in m")
ax.set_title(f"Ball with mass {m}kg, initial speed {v_init}m/s and r = {100*r:.0f}cm")
ax.legend()
ax.set_ylim(bottom = 0)
plt.show()
print(f"Without air resistance, it reached {max(heights_noair):.2f} meters.")
print(f"With air resistance, it reached {max(heights_air):.2f} meters.")
print(f"That is {max(heights_noair) / max(heights_air):.2f} higher")
print(f"It took {len(times_noair)*dt:.2f} seconds to reach the ground without air resistance")
print(f"With air resistance it took {len(times_air)*dt:.2f} seconds.")
print(f"That is {len(times_noair) / len(times_air):.3f} times longer.")
