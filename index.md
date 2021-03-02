## Welcome to my Portfolio!

Hi there! My name is Tommy and I enjoy programming, with a particular interest in object-oriented programming. Here you will find a mix of various personal projects I have created. I deeply enjoy mathematics and am trying to create algorithms that solve different problems concerning limits, derivatives, and integration. These codes will also show graphs where possible to help a user visualize the calculated quantities. There are also some other projects that I have put here just for fun. Have a look! You are welcome to use and modify any of these codes however you wish.

## Function Graphing

The preliminary section in most calculus textbooks reviews the student on the ways to graph a function via point plotting. This can be tedious so a calculator certainly comes in handy. Not only that, but knowing what a function graphically looks like can be a powerful tool for intuitive understanding. Graphing will be utilized in the following codes so this is a good starting point for someone new to coding.

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
Refer to matplotlib [documentation](https://matplotlib.org/stable/contents.html) for further graph customization

## Example of how to Embed a link in text : [editor on GitHub](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/edit/main/index.md)
