## Welcome to my Portfolio!

Hi there! My name is Tommy and I enjoy programming, with a particular interest in object-oriented programming. Here you will find a mix of various personal projects I have created. I deeply enjoy mathematics and am trying to create algorithms that solve different problems concerning limits, derivatives, and integration. These codes will also show graphs where possible to help a user visualize the calculated quantities. There are also some other projects that I have put here just for fun. Have a look! You are welcome to use and modify any of these codes however you wish.

## Senior Project Physics 2019-2020

For my senior project I worked with Dr. Lloyd Bumm and his research group at the University of Oklahoma. I picked up the vibrational analysis project which had previously been built up by two students prior to me, Elizabeth Moffett and Jake Burcham. My role was to modify existing Matlab code to continuously acquire data with a DT-8904 DAQ attached to an S-13 Geophone seismometer. Once that experiment was setup, I was tasked with updating our data acquisition system using a UEIPAC 300-1G-02-08-00-PA cube. This involved modifying source code in C to continuously acquire data, and simultaneously save data files every hour. For troubleshooting, the binary files in C were transferred to Matlab where they could be viewed graphically or with a table. The following PDF summarizes the work I did from Fall 2019 to Spring 2020, although I continued to work on the project until December 2020, and still correspond to troubleshooting inquiries.

[Beauchamp_Capstone.2020_05_11_FINAL.pdf](https://github.com/Tommy-Beauchamp/Tommy-Beauchamp.github.io/files/6103366/Beauchamp_Capstone.2020_05_11_FINAL.pdf)

## Function Graphing

The preliminary section in most calculus textbooks reviews the student on the ways to graph a function via point plotting. This method is often tedious, so a graphing calculator certainly comes in handy. Knowing what a function looks like graphically can also be a powerful tool for building intuitive understanding. The user specifies a function to graph, and then a domain over which they want to see the plot.

```python
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

```python
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

## Analytical Limit and Continuity Evaluation

This project was an exciting trek into the Sympy library which allows for symbolic maths to be performed by the computer, as opposed to numerical calculations. This program contains a continuity check class, which takes an algebraic function from the user, and a point to be checked for continuity. Using the limit calculation capabilities of the Sympy library, the left and right hand limits are calculated for the function and the properties of continuity are employed to classify the function as either continuous or discontinuous at the point. Furthermore, if the function possesses a discontinuity at the point, the program classifies it as a removable or nonremovable discontinuity. Finally, the function is graphed over a specified window, and the removable discontinuity is redefined and plotted if possible.

```python
import matplotlib.pyplot as plt
import numpy as np
import sympy as sym
import sys

x = sym.Symbol('X')
sym.init_printing(use_unicode=False, wrap_line=True)

class Continuity_Check:

    def __init__(self, func_variable, expression, limit_value):
        self.x = func_variable
        self.exp = expression
        self.lim = limit_value

    def func(self):
        return (self.exp)

    def func_continuity_test(self):

        def func(self):
            return (self.exp)

        try:
            d = func(self).subs(self.x, self.lim)
        except ValueError:
            print("Function does not exist at " + str(self.x) + " = " + str(self.lim) + ".")
            d = "DNE"

        print("Limit of " + str(func(self)) + " as " + str(self.x) + " approaches " + str(self.lim) +
              " from the left side is: ")  
        print(sym.limit(func(self), self.x, self.lim, "-"))
        a = sym.limit(func(self), self.x, self.lim, "-")

        print("Limit of " + str(func(self)) + " as " + str(self.x) + " approaches " + str(self.lim) + 
            " from the right side is: ")
        print(sym.limit(func(self), self.x, self.lim, "+"))
        b = sym.limit(func(self), self.x, self.lim, "+")
       
        if a == b:
            print("Limit of " + str(func(self)) + " as " + str(self.x) + " approaches " + str(self.lim) + 
                  " from both sides is: ")
            print(sym.limit(func(self), self.x, self.lim, "+-"))
            c = sym.limit(func(self), self.x, self.lim, "+-")

        else:
            print("The function: " + str(func(self)) + " has a nonremovable discontinuity at the point "
                  + str(self.x) + " = " + str(self.lim) + ".")

        if ((a == sym.oo) and (b == sym.oo)) or ((a == -1 * sym.oo) and (b == -1 * sym.oo)):
            print("The function: " + str(func(self)) + " has a nonremovable discontinuity at the point "
                  + str(self.x) + " = " + str(self.lim) + ".")

        elif (a == b) and (str(c) != str(d)):
            print("The function " + str(func(self)) + " has a removable discontinuity at the point "
                  + str(self.x) + " = " + str(self.lim) + ".")

            print("Redefine the function " + str(func(self)) + " to be " + str(c) + " at " + str(self.x) + " = " + str(self.lim) + ".")

        elif (a == b) and (str(c) == str(d)):
            print("The function " + str(func(self)) + " is continuous at " + str(self.x) + " = " + str(self.lim) + ".")

        return d

limit_value = 2
r = Continuity_Check(x, x**2, limit_value)
graph = r.func()
f_val = r.func_continuity_test()

x_start = -9.99
x_end = 10
xDataLeft = np.arange(x_start, limit_value, 0.1)
xDataRight = np.arange(limit_value + 0.1, x_end, 0.1)
yDataLeft = []
yDataRight = []
for element in xDataLeft:
    yDataLeft.append(graph.subs(x, element))

for element in xDataRight:
    yDataRight.append(graph.subs(x, element))

plt.plot(xDataLeft, yDataLeft, 'b', label='Calculated Points')
plt.plot(xDataRight, yDataRight, 'b')

if (sym.limit(graph, x, limit_value, "+") == (sym.oo)) or (sym.limit(graph, x, limit_value, "+") == (-1 * (sym.oo))):
    print("Cannot plot point due to infinite discontinuity")
elif (sym.limit(graph, x, limit_value, "-") == (sym.oo)) or (sym.limit(graph, x, limit_value, "-") == (-1 * (sym.oo))):
    print("Cannot plot point due to infinite discontinuity")
else:
    plt.plot(limit_value, sym.limit(graph, x, limit_value, "+-"), 'ro', label='Limit Value')
        
plt.xlabel("x")
plt.ylabel("f(x)")
plt.legend()
plt.show()
```

## Experimental Physics Curve Fitting

The following is a curve fitting code I wrote for an experiment I conducted to measure the lifetime of muons as they descend to the surface from Earth's upper atmosphere. This code utilizes scipy to fit a model to a scatter plot, and then everything is plotted on a single graph using matplotlib. I have annotated this code with comments, and have also attached the text document (see below) with the raw data I used for the fit. Note that you will want to place this file where your preferred IDE can access it. Physics students may find the template of this fitting code useful for other experiments they wish to conduct, as the process is very much the same. Load your raw data, sort the respective values into lists, and then fit a scatter plot of that data to a desired model. As always, feel free to use and modify this code as you see "fit".

```python
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

## Rock Paper Scissors

This project is a simple game that includes some functions from different libraries and incorporates the use of a class to keep everything organized. There are also a few try and except portions to prevent the code from crashing, as it takes user input that needs to be of a specific type. The code starts by prompting the user for their name and the number of rounds they would like to play. The game begins with a countdown using sleep from the time package. The user selects one of the possible moves and the computer randomly generates a counter move. The moves are compared according to the rules of the game and the score from each round is kept. After all the rounds are played the final score and winner are presented. In the event of a tie, a series of tie breaker rounds are played until someone scores a point.

```python
import random as rn
import time
import sys

possible_choices = [1, 2, 3]
i = 0
player_score = 0
computer_score = 0
winner_found = False

player_name = input("Enter Your Name: ")

while True:
    try:
        rounds = int(input("How many rounds would you like to play?: "))
        if rounds > 0:
            break
        else:
            raise ValueError("Please pick a positive integer.")
    except ValueError as ve:
        print(ve)

def player_move(player_choice):
    if player_choice == 1:
        player_choice = "Rock"
    elif player_choice == 2:
        player_choice = "Paper"
    else:
        player_choice = "Scissors"
    return player_choice

def computer_move(computer_choice):
    if computer_choice == 1:
        computer_choice = "Rock"
    elif computer_choice == 2:
        computer_choice = "Paper"
    else:
        computer_choice = "Scissors"
    return computer_choice

def game():
    
    user_input = -1

    print("3...")
    time.sleep(1)
    print("2...")
    time.sleep(1)
    print("1...")
    time.sleep(1)

    print("Enter one of the follwing numbers: ")
    while True:
        try:
            user_input = int(input("1. Rock     2. Paper     3. Scissors "))
            if (user_input - 1) == possible_choices.index(user_input):
                break
        except ValueError:
            print("Input must be an integer: '1' for Rock, '2' for Paper, '3' for Scissors")
    return user_input

def game_over(player_final_score, computer_final_score):
    print("Final Score")
    print("" + player_name + ": " + str(player_score) + "")
    print("Computer: " + str(computer_score) + "")
    if player_score > computer_score:
        print("" + player_name + " Wins!")
    else:
        print("Computer Wins!")
    return


class Outcome:

    def __init__ (self, pm, cm, ps, cs):
        self.player = pm
        self.computer = cm
        self.player_score = ps
        self.computer_score = cs

    def outcome(self):

        # Player chose Rock
        if self.player == "Rock" and self.computer == "Rock":
            print("" + player_name + " chose Rock and Computer chose Rock. No winner.")

        elif self.player == "Rock" and self.computer == "Paper":
            print("" + player_name + " chose Rock and Computer chose Paper. Paper covers Rock.")
            print("Computer wins!")
            self.computer_score += 1

        elif self.player == "Rock" and self.computer == "Scissors":
            print("" + player_name + " chose Rock and Computer chose Scissors. Rock beats Scissors")
            print("" + player_name + " wins!")
            self.player_score += 1

        # Player chose Paper
        elif self.player == "Paper" and self.computer == "Rock":
            print("" + player_name + " chose Paper and Computer chose Rock. Paper covers Rock.")
            print("" + player_name + " wins!")
            self.player_score += 1

        elif self.player == "Paper" and self.computer == "Paper":
            print("" + player_name + " chose Paper and Computer chose Paper. No winner.")

        elif self.player == "Paper" and self.computer == "Scissors":
            print("" + player_name + " chose Paper and Computer chose Scissors. Scissors cut Paper")
            print("Computer wins!")
            self.computer_score += 1

        # Player chose Scissors
        elif self.player == "Scissors" and self.computer == "Rock":
            print("" + player_name + " chose Scissors and Computer chose Rock. Rock beats Scissors.")
            print("Computer wins!")
            self.computer_score += 1

        elif self.player == "Scissors" and self.computer == "Paper":
            print("" + player_name + " chose Scissors and Computer chose Paper. Scissors cut Paper.")
            print("" + player_name + " wins!")
            self.player_score += 1

        else:
            print("" + player_name + " chose Scissors and Computer chose Scissors. No winner")

    def score_p(self):
        print("Player score is " + str(self.player_score))
        return self.player_score

    def score_c(self):
        print("Computer score is " + str(self.computer_score))
        return self.computer_score


while i < rounds:
    print("\n")
    player_choice = game()
    x = player_move(player_choice)
    y = computer_move(rn.randint(1,3))

    result = Outcome(x,y, player_score, computer_score)
    print("\n")
    result.outcome()
    player_score = result.score_p()
    computer_score = result.score_c()
    i += 1

    input("Press Enter to proceed: ")

print("\n")
while winner_found == False:
    if player_score != computer_score:
        game_over(player_score, computer_score)
        winner_found = True
    else:
        print("Game is currently tied. Initializing tie breaker round.")
        print("\n")
        player_choice = game()
        x = player_move(player_choice)
        y = computer_move(rn.randint(1,3))

        result = Outcome(x,y, player_score, computer_score)
        print("\n")
        result.outcome()
        player_score = result.score_p()
        computer_score = result.score_c()
```
