# Exercises for Day 3
Numpy and inheritance

## 1. Numpy exercises

#### a. Create a null vector of size 10 but the fifth value which is 1
```
>>> import numpy as np
>>> x = np.zeros(10)
>>> print(x)
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
>>> x[5]=1
>>> print(x)
[0. 0. 0. 0. 0. 1. 0. 0. 0. 0.]
>>> 
```

#### b. Create a vector with values ranging from 10 to 49
```
>>> y = np.arange(10,50)
>>> print(y)
[10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33
 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49]
```

#### c. Reverse a vector (first element becomes last) 
```
>>> y_flip = np.flip(y)
>>> print(y_flip)
[49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26
 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10]
>>> 
```

#### d. Create a 3x3 matrix with values ranging from 0 to 8
```
>>> 
>>> z = np.matrix('0 1 2;3 4 5;6 7 8')
>>> print(z)
[[0 1 2]
 [3 4 5]
 [6 7 8]]
>>> 
```

#### e. Find indices of non-zero elements from [1,2,0,0,4,0]
```
>>> 
>>> a = np.array([1,2,0,0,4,0])
>>> a
array([1, 2, 0, 0, 4, 0])
>>> np.nonzero(a)
(array([0, 1, 4]),)
>>> 
```

#### f. Create a random vector of size 30 and find the mean value
```
>>> 
>>> b = np.random.randint(10, size=30)
>>> print(b)
[9 6 0 7 6 8 5 6 1 5 1 0 2 1 1 4 8 1 4 6 0 4 2 4 4 1 5 6 8 0]
>>> 
```

#### g. Create a 2d array with 1 on the border and 0 inside
```
>>> 
>>> c = np.array([[1,0,1],[1,0,1]])
>>> print(c)
[[1 0 1]
 [1 0 1]]
>>> 
```

#### h. Create a 8x8 matrix and fill it with a checkerboard pattern
```
>>> d=np.zeros((8,8),dtype=int)
>>> d
array([[0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0, 0, 0, 0]])
>>> d[1::2,::2]=1
>>> d[::2,1::2]=1
>>> d
array([[0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0]])
>>> 
```

#### i. Create a checkerboard 8x8 matrix using the tile function
```
>>> e = np.array([0,1])
>>> f = np.array([1,0])
>>> e = np.tile(e,4)
>>> f = np.tile(f,4)
>>> e
array([0, 1, 0, 1, 0, 1, 0, 1])
>>> f
array([1, 0, 1, 0, 1, 0, 1, 0])
>>> np.array([e,f,e,f,e,f,e,f])
array([[0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0],
       [0, 1, 0, 1, 0, 1, 0, 1],
       [1, 0, 1, 0, 1, 0, 1, 0]])
>>> 
```

#### j. Given a 1D array, negate all elements which are between 3 and 8, in place
```
>>> Z = np.arange(11)
>>> Z[3:9] = -Z[3:9]
>>> print(Z)
[ 0  1  2 -3 -4 -5 -6 -7 -8  9 10]
>>> 
```

#### k. Create a random vector of size 10 and sort it
```
>>> Z = np.random.random(10)
>>> print(Z)
[0.92618771 0.97113846 0.96094107 0.3193512  0.89976998 0.20828836
 0.97372115 0.2743059  0.37525662 0.79225523]
>>> Z = np.sort(Z)
>>> print(Z)
[0.20828836 0.2743059  0.3193512  0.37525662 0.79225523 0.89976998
 0.92618771 0.96094107 0.97113846 0.97372115]
>>> 
```

#### l. Consider two random array A anb B, check if they are equal
```
>>> A = np.random.randint(0,2,5)
>>> B = np.random.randint(0,2,5)
>>> equal = np.array_equal(A,B)
>>> print(equal)
False
```

#### m. How to convert an integer (32 bits) array into a float (32 bits) in place?
```
>>> Z = np.arange(10, dtype=np.int32)
>>> print(Z.dtype)
int32
>>> print(Z)
[0 1 2 3 4 5 6 7 8 9]
>>> Z = np.float32(Z)
>>> print(Z.dtype)
float32
>>> 
```

#### n. How to get the diagonal of a dot product?
Sorry, I couldnt do this. Mainly because I do not understand the math...
```
A = np.arange(9).reshape(3,3)
B = A + 1
C = np.dot(A,B)
D = ...
print(D)
```

## 2. Speed optimization using Numpy
Revisit the ```matmult.py``` example from yesterday and improve its performance using Numpy.
```
# Program to multiply two matrices using nested loops
##import random
#imported numpy instead of random
import numpy as np

N = 250

# NxN matrix
X = []
for i in range(N):
    #added a numpy function instead
    X.append([np.random.randint(100) for r in range(N)])
    #X.append([random.randint(0,100) for r in range(N)])
	
# Nx(N+1) matrix
Y = []
for i in range(N):
    #added a numpy function instead
    Y.append([np.random.randint(100) for r in range(N+1)])
    #Y.append([random.randint(0,100) for r in range(N+1)])

# result is Nx(N+1)
result = []
for i in range(N):
    result.append([0] * (N+1))

# iterate through rows of X
for i in range(len(X)):
    # iterate through columns of Y
    for j in range(len(Y[0])):
        # iterate through rows of Y
        for k in range(len(Y)):
            result[i][j] += X[i][k] * Y[k][j]

for r in result:
    print(r)
```

## 3. Examples on classes and inheritance in Python

#### a. Create a "Person" class which takes firstname and lastname as arguments to the constructor (```___init___```) and define a method that returns the full name of the person as a combined string.
```
class Person:
    def __init__(self,first,last):
        self.first = first
        self.last = last

    def name(self):
        return self.first + " " + self.last

a=Person('Gustaf','Peterson')
print(a.name())
```

#### b. Create a "Student" class which inherits from the "Person" class, takes the subject area as an additional argument to the constructor and define a method that prints the full name and the subject area of the student.
```
class Person:
    def __init__(self,first,last,student):
        self.first = first
        self.last = last
        self.student = student
        
    def name(self):
        return self.first + " " + self.last

    def subject(self):
        return self.student
a=Person('Gustaf','Peterson','geology')

print(a.name())
print(a.subject())
```

#### c. You should be able now to use your "Student" class like this:
```
In [1]: from classroom import Student
In [2]: me = Student('Benedikt', 'Daurer', 'physics') 
In [3]: me.printNameSubject() 
Benedikt Daurer, physics
```

#### d. Create a "Teacher" class which also inherits from "Person", takes the name of the course (e.g. Python programming) as an argument and define a method that prints the full name of the teacher and the course he teaches. 
```
class Person:
    def __init__(self,first,last,student,teatcher):
        self.first = first
        self.last = last
        self.student = student
        self.teatcher = teatcher

    def name(self):
        return self.first + " " + self.last

    def subject(self):
        return self.student

    def course(self):
        return self.teatcher

student=Person('Gustaf','Peterson','geology','python programming')
teatcher=Person('Filipe','Maia','science','python programming')

print(student.name())
print(student.subject())

print(teatcher.name()+" "+teatcher.course())
```
