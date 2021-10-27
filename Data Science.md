# Data Science

## IPython shortcuts

- ? , help of a command len?
- """ create a docstring with those"""
- ?? , access source code
- .<TAB> gives all the available attributes, functions of an obj



## Navigation Shortcuts

- ctl + a , move start of line
- ctrl + e, move end of line
- ctrl + b or ctrl left arrow , move one word left
- ctrl + f or ctrl right arrow, move one word right 
- ctrl + d , delete next character
- ctrl +k , cut text from cursor
- ctrl + u, paste text that was cut
- ctrl + t, switch previous 2 characters

# Numpy

## Intro

It is so efficient to use numpy arrays instead of normal python lists because python lists are actually c structures that refere to a pointer object that refer to a structure, while numpy array is more efficent as it only refers to a one pointer







## Linear Regression

Relationship between variables x and y, creating a line

it tries to minimize the residuals( the points distance to the line)
we dum the redisuals (turning them to positive values squaring the residuals), the sum of the squared residuals.
Linear regression tried to minimize this number.

## Gradiant Decent

Optimization technique, predict, calculate error, learning step(adjusting our initial prediction, learn from mistakes )
Optimization algo to find the minimum of a function

Gradiant is the slope 

Parameters

- starting point
- learning rate
- temp value 

## Cost Function

The sum of square residuals used in Linear Regression is an example of a cost function. They are also called Loss Functions or objective functions 







```python
import numpy as np 
```

