# Basic-Monte-Carlo-integrator
Apply set theoretic operations to various shapes, and compute the volume of the resulting shape using Monte Carlo approximation.

Basic shapes, and intersection:
```
shape1 = Triangle([[0,0],[4,4],[3,4]])  #prescribe triangle by prescribing its vertices as a list of length two lists
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


<img width="469" alt="Screenshot 2025-01-06 at 12 36 13 PM" src="https://github.com/user-attachments/assets/04dfcb88-b848-45f1-a896-0281238b53af" />

```
Volume = 0.0708
```

Applying other operations:

```
shape = ((shape1 + shape2) - shape4)^shape3 #union, set difference, and symmetric difference (symmetric difference = A+B - A*B)
shape()
```

<img width="440" alt="Screenshot 2025-01-06 at 12 41 17 PM" src="https://github.com/user-attachments/assets/88618cc1-8a91-4f08-ac0b-417d3d023ecb" />


We can also use + to translate a shape by a vector, and * to scale it by a factor:

```
shape = shape + [1,2] # translate your shape by vector [1,2]
shape()
shape = [1,2] + shape #can also translate from the left
# beware that + is not associative now, if using both Shape + Shape and Shape + vector

shape = (2*shape)*3 #scale your shape from the left or from the right
shape()
```

<img width="430" alt="Screenshot 2025-01-06 at 12 42 50 PM" src="https://github.com/user-attachments/assets/8acd1e31-c158-4e39-86fb-b8cd1387c358" />

<img width="432" alt="Screenshot 2025-01-06 at 12 43 05 PM" src="https://github.com/user-attachments/assets/84c22b94-dc5b-4551-b336-29aa1c6734b0" />

The ambient rectangle used for Monte Carlo approximation is automatically adjusted. You can prescribe it to be whatever you want using the adjust_box method.


<br>  

Another example:

```
shape = Disk(1,center = [1,1])
lst = [shape.rotate(60*i) for i in range(6)]
new_shape = sum(lst, EmptyShape()) - shape.translate([-1,-1])   #use EmptyShape(dimension = 2 by default) to initialize sum
new_shape.adjustbox([[-3,3],[-3,3]])
new_shape.plot()
```

<img width="446" alt="Screenshot 2025-01-06 at 12 44 59 PM" src="https://github.com/user-attachments/assets/8ee42f72-b808-432c-9a1c-e31e5bcd48c9" />

<br> <br>

Iterating, shifting, rotating, and taking union:

<img width="451" alt="Screenshot 2025-01-06 at 12 45 34 PM" src="https://github.com/user-attachments/assets/0d8a4982-18e2-4fe4-a103-ac52146d090c" />






