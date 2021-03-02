## Welcome to my Portfolio!

Hi there! My name is Tommy and I am learning how to code, with a particular interest in object-oriented programming. Here you will find a mix of various personal projects I have created. I deeply enjoy mathematics and am trying to create algorithms that solve different problems concerning limits, derivatives, and integration. These codes will also show graphs where possible to help a user visualize the calculated quantities. There are also some other projects that I have put here just for fun. Have a look! You are welcome to use and modify any of these codes however you wish.

## Example of how to Embed a link in text : [editor on GitHub](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/edit/main/index.md)

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown

import math
import matplotlib.pyplot as plt
import numpy as np

# input the function of a single variable that you wish to graph
# math is imported for access to more functions

def func_calc(x):
    return math.sqrt(x)
# This specifies a function and allows it to recieve multiple inputs with function calls


x_start = 0                                   # Specify a domain with x_start to x_end
x_end = 9

y_values = []                                 # Creates an empty list to hold the calculated 
                                              # y-values for each point in the domain

x_values = np.arange(x_start, x_end, 0.1)     # Creates a list of x-values in a numpy array
                                              # based on the previously stated domain
                                              # third argument tells numpy array how to increment

for element in x_values:
    y_values.append(func_calc(element))       # This for loop looks at each of the elements
                                              # in the x-value array and calculates the function
                                              # value at each of those points
                                              # calculated values appended to y-value list

plt.plot(x_values, y_values, 'b', label='Function Graph')
plt.xlabel("x")
plt.ylabel("f(x)")
plt.legend()
plt.show()

# Refer to matplotlib documentation for further graph customization
# https://matplotlib.org/stable/contents.html

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
