# Basic-Monte-Carlo-integrator
Apply set theoretic operations to various shapes, and compute the volume of the resulting shape using Monte Carlo approximation.

Basic shapes, and intersection:
```
shape1 = Triangle([[0,0],[2,4],[15,4]])  #prescribe triangle but prescribing its vertices as a list of length two lists
shape2 = Rectangle([[1,2],[3,4]])  #prescribe rectangle by prescribing its projections to each axis as a list of lists
shape3 = Disk(1) # disk of radius 1. Default dimension is 2, and default center is [0,0,...,0]
shape4 = Disk(5, 2, [-1,-1])    #parameters are (radius, dimension, center). 
shape5 = Ellipsoid([2,3], 2, [1,1])  #more generally we can prescribe (interior of) ellipsoid: here the semiaxes are (2,3), dimension 2, center [1,1]: x^2/2^2 + y^2/3^2 < 1. Dimension is asked for to avoid necessity to input center if one wants origin as center.
shape6 = GraphSide([1,2],"above") # One side of the graph of y = 2x + 1. Second parameter is "above" or "below".

shape = shape1 * shape3 #intersection of two shapes
shape() #call a shape to plot it
shape.plot() #or call the plot function
shape(volume = True) #include extra parameter to also get its Monte-Carlo computed volume
```

<img width="473" alt="Screenshot 2025-01-06 at 3 37 20 PM" src="https://github.com/user-attachments/assets/47b35ab2-5eb7-4d1d-9f73-f7ecef840ff3" />



```
Volume = 0.0708
```

Applying other operations:

```
shape = ((shape1 + shape2) - shape4)^shape3 #union, set difference, and symmetric difference (symmetric difference = A+B - A*B)
shape()
```

<img width="567" alt="Screenshot 2025-01-06 at 3 37 28 PM" src="https://github.com/user-attachments/assets/b81ab120-319d-40fb-b120-52fc2e373b61" />



We can also use + to translate a shape by a vector, and * to scale it by a factor:

```
shape = ((shape1 + shape2) - shape4)^shape3 #union, set difference, and symmetric difference (symmetric difference = A+B - A*B)
shape()

shape7 = shape + [50,70] # translate your shape by vector [1,2]
shape()
shape7 = [40,60] + shape7 #can also translate from the left
# beware that + is not associative now, if using both Shape + Shape and Shape + vector

shape8 = (2*shape)*3 #scale your shape from the left or from the right
(shape7+shape8)()
```

<img width="369" alt="Screenshot 2025-01-06 at 3 40 26 PM" src="https://github.com/user-attachments/assets/a285e2bc-76c4-4dd5-921b-e91f31bb87be" />


The ambient rectangle used for Monte Carlo approximation is automatically adjusted. You can prescribe it to be whatever you want using the adjustbox method.


<br>  

Another example:

```
shape = Disk(1,center = [1,1])
lst = [shape.rotate(60*i) for i in range(6)]
new_shape = sum(lst, EmptyShape()) - (shape+[-1,-1])   #use EmptyShape(dimension = 2 by default) to initialize sum
# alternatively, we can translate by e.g. shape.translate([-1,-1]), and similarly for scaling. These methods have an optional in_place parameter.
new_shape.adjustbox([[-3,3],[-3,3]])
new_shape.plot()
```

<img width="446" alt="Screenshot 2025-01-06 at 12 44 59 PM" src="https://github.com/user-attachments/assets/8ee42f72-b808-432c-9a1c-e31e5bcd48c9" />

<br> <br>

Iterating, shifting, rotating, and taking union:

<img width="451" alt="Screenshot 2025-01-06 at 12 45 34 PM" src="https://github.com/user-attachments/assets/0d8a4982-18e2-4fe4-a103-ac52146d090c" />






