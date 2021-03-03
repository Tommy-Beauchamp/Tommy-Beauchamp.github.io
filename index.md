## Welcome to my Portfolio!

Hi there! My name is Tommy and I enjoy programming, with a particular interest in object-oriented programming. Here you will find a mix of various personal projects I have created. I deeply enjoy mathematics and am trying to create algorithms that solve different problems concerning limits, derivatives, and integration. These codes will also show graphs where possible to help a user visualize the calculated quantities. There are also some other projects that I have put here just for fun. Have a look! You are welcome to use and modify any of these codes however you wish.

## Function Graphing

The preliminary section in most calculus textbooks reviews the student on the ways to graph a function via point plotting. This method can be tedious so a graphing calculator certainly comes in handy. Knowing what a function graphically looks like can also be a powerful tool for building intuitive understanding.

```markdown
import math
import matplotlib.pyplot as plt
import numpy as np

def func_calc(x):
    return math.sqrt(x)

x_start = 0
x_end = 9
y_values = []                               
x_values = np.arange(x_start, x_end, 0.1)

for element in x_values:
    y_values.append(func_calc(element))

plt.plot(x_values, y_values, 'b', label='Function Graph')
plt.xlabel("x")
plt.ylabel("f(x)")
plt.legend()
plt.show()
```
Refer to [matplotlib documentation](https://matplotlib.org/stable/contents.html) for further graph customization.

## Numerical Limit Calculations

When limits are first introduced informally, we aren't given the toolkit to evaluate them analytically with our algebra tricks. This leaves students with either a graphical analysis or a numerical method. If you're anything like me, you know how annoying it can be to create the numerical tables by hand to see what values our function tends towards as we approach some input value. This project was born out of that frustration. 

The user specifies a function, an input value to approach, how many decimals they want to have their table go to (3 decimals in this case would be 0.1, 0.01, and 0.001 from the right of 0), and then a domain over which they want to graph the function. If the function possesses a discontinuity at the limit value, the code will recognize this and remove the point from the graphing process. The result prints the left and right hand limit values to the console and then shows a graph with either the limit value, or the left and right limits near the input of interest.

```markdown
import math
import matplotlib.pyplot as plt
import numpy as np

def func_calc(x):
    return x ** 2


def left_limits(x):
    i = 1
    print("Left hand limit to " + str(desired_precision) + " decimal places...")
    while i <= desired_precision:
       left_point = x - ((10 ** -i))
       print(func_calc(left_point))
       i += 1
    left_result = func_calc(left_point)
    print("Left hand limit is " + str(left_result))
    return left_result


def right_limits(x):
    i = 1
    print("Right hand limit to " + str(desired_precision) + " decimal places...")
    while i <= desired_precision:
       right_point = x + ((10 ** -i))
       print(func_calc(right_point))
       i += 1
    right_result = func_calc(right_point)
    print("Right hand limit is " + str(right_result))
    return right_result

limit_point = 0
desired_precision = 3

x_start = -1.99
x_end = 2
y_values = []

x_values = np.arange(x_start, x_end, 0.01)

for element in x_values:
    y_values.append(func_calc(element))

try:
    print("The function at x = " + str(limit_point) + " is " + str(func_calc(limit_point)))
except:
    print("Function is undefined at the point x = " + str(limit_point))

print("\n")

left_limits(limit_point)
print("\n")
right_limits(limit_point)
print("\n")

plt.plot(x_values, y_values, 'b', label='Calculated Points')
try:
    plt.plot(limit_point, func_calc(limit_point), 'ro', label='Limit Value')
except:
    plt.plot(limit_point - (10 ** - (desired_precision)), func_calc(limit_point - (10 ** - (desired_precision))), 'ro', label='Left Limit Value')
    plt.plot(limit_point + (10 ** -(desired_precision)), func_calc(limit_point + (10 ** - (desired_precision))), 'go', label='Right Limit Value')
plt.xlabel("x")
plt.ylabel("f(x)")
plt.legend()
plt.show()
```

## Experimental Physics Curve Fitting

The following is a curve fitting code I wrote for an experiment I conducted to measure the lifetime of muons as they descend to the surface from Earth's upper atmosphere. This code utilizes scipy to fit a model to a scatter plot, and then everything is plotted on a single graph using matplotlib. I have annotated this code with comments, and have also attached the text document (see below) with the raw data I used for the fit. Note that you will want to place this file where your preferred IDE can access it. Physics students may find the template of this fitting code useful for other experiments they wish to conduct, as the process is very much the same. Load your raw data, sort the respective values into lists, and then fit a scatter plot of that data to a desired model. As always, feel free to use and modify this code as you see "fit".

```markdown
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# Exponential Decay of Lifetime Model

import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# Exponential Decay of Lifetime Model

def func(x, a, b, c):
    return a*np.exp(-x/b)+c

Bins = 25 # Number of histogram bins

lifetime_array = [] # List to hold all recorded decay times
discriminator_array = [] # Certain times are used for the fit

sigma_array = [] # List to hold error calculations

f = open("MuonLongData.txt", 'r') # open file of interest

# sort the values in the file into a large list

for element in f.readlines():
    lifetime_array.append(int(element))

# pick only desired time values and sort into smaller list

for data in lifetime_array:
    if data < 40000:
        discriminator_array.append(data)

# get number of counts and bin edges in each bin from histogram and print for verification

counts, bin_edges = np.histogram(discriminator_array, bins=Bins)

# sort count numbers and bin edges into an array

xBins = bin_edges
xData = np.array(xBins)
xData = np.delete(xData, 0)  # using the bin edges creates one more x-value than data points
xData = np.delete(xData, -1) # the first value is thrown away and the last x-value omitted
yData = np.array(counts)
yData = np.delete(yData, 0)
square_root_counts = np.sqrt(yData)
sigma_array = yData/square_root_counts # Weights the data points, according to number of counts

# make a guess at parameters a, b, c

InitialGuess = [1500, 200, 0.0]

plt.scatter(xData, yData, s=15, c='red', label='Experimental Data: Counts per Bin')
plt.xlabel('Time (ns)')
plt.ylabel('Counts')
plt.yscale('log') # For better viewing

popt, pcov = curve_fit(func, xData, yData, InitialGuess, sigma=sigma_array, absolute_sigma=True) # Fitting Tool

print(popt) # Fit Parameters
print(pcov) # Variance of Fit Parameters
print(np.sqrt(np.diag(pcov))) # Standard Error of Fit Parameters

xFit = np.arange(0.0, 20000, 100) # Domain for a fitting graph
plt.plot(xFit, func(xFit, *popt), 'g', label='Weighted Fit')

# Error Bars

yerror = sigma_array
plt.errorbar(xData, yData, yerr=yerror, fmt=' ', c='black')
plt.xlabel('Time (ns)')
plt.ylabel('Counts')
plt.legend()
plt.show()

f.close()
```
[MuonLongData.txt](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/files/6077130/MuonLongData.txt)


## Example of how to Embed a link in text : [editor on GitHub](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/edit/main/index.md)
