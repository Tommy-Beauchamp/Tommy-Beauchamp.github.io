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

The user specifies a function, an input value to approach, how many decimals they want to have their table go to (3 decimals would be something like 11.9, 11.99, 11.999), and then a domain over which they want to graph the function. If the function possesses a discontinuity at the limit value, the code will recognize that and remove the point from the graphing process. The result prints the left and right hand limit values and also shows a graph with either the limit value if it is defined in the function's domain or the left and right limits.

```markdown
import math
import matplotlib.pyplot as plt
import numpy as np

def func_calc(x):
    return (abs(x + 1) - abs(x - 1))/(x)


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
desired_precision = 4

x_start = -5.99
x_end = 6
y_values = []
m = 0

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

## Example of how to Embed a link in text : [editor on GitHub](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/edit/main/index.md)
