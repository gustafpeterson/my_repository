# Exercises for Day 2
Organising, debugging and profiling Python code

## 1. Creating a Python package
Following the slides 19/20 from this morning's session, we will create an **animals** package.

> Please note that with Python 3, implicit relative imports are no longer supported [https://www.python.org/dev/peps/pep-0328/](https://www.python.org/dev/peps/pep-0328/)

#### a. Create a directory for package

#### b. Add the modules ```birds.py``` and ```mammals.py``` into your package directory
```
./test_animals:
total 16
drwxr-xr-x 3 gustaf gustaf 4096 mar 25 18:17 .
drwxr-xr-x 3 gustaf gustaf 4096 mar 25 18:18 ..
drwxr-xr-x 4 gustaf gustaf 4096 mar 25 18:16 animals
-rw-rw-r-- 1 gustaf gustaf  588 mar 24 14:50 test_animals.py

./test_animals/animals:
total 32
drwxr-xr-x 4 gustaf gustaf 4096 mar 25 18:16 .
drwxr-xr-x 3 gustaf gustaf 4096 mar 25 18:17 ..
-rw-rw-r-- 1 gustaf gustaf  325 mar 24 14:19 birds.py
drwxr-xr-x 3 gustaf gustaf 4096 mar 24 14:50 dangerous
-rw-rw-r-- 1 gustaf gustaf  327 mar 24 14:42 fish.py
drwxr-xr-x 3 gustaf gustaf 4096 mar 24 14:49 harmless
-rw-rw-r-- 1 gustaf gustaf   77 mar 24 14:42 __init__.py
-rw-rw-r-- 1 gustaf gustaf  334 mar 24 13:45 mammals.py

./test_animals/animals/dangerous:
total 28
drwxr-xr-x 3 gustaf gustaf 4096 mar 24 14:50 .
drwxr-xr-x 4 gustaf gustaf 4096 mar 25 18:16 ..
-rw-rw-r-- 1 gustaf gustaf  325 mar 24 14:19 birds.py
-rw-rw-r-- 1 gustaf gustaf  327 mar 24 14:42 fish.py
-rw-rw-r-- 1 gustaf gustaf   77 mar 24 14:42 __init__.py
-rw-rw-r-- 1 gustaf gustaf  313 mar 24 14:46 mammals.py

./test_animals/animals/harmless:
total 28
drwxr-xr-x 3 gustaf gustaf 4096 mar 24 14:49 .
drwxr-xr-x 4 gustaf gustaf 4096 mar 25 18:16 ..
-rw-rw-r-- 1 gustaf gustaf  325 mar 24 14:19 birds.py
-rw-rw-r-- 1 gustaf gustaf  327 mar 24 14:42 fish.py
-rw-rw-r-- 1 gustaf gustaf   77 mar 24 14:42 __init__.py
-rw-rw-r-- 1 gustaf gustaf  322 mar 24 14:46 mammals.py
```

#### c. Add ```__init__.py``` module to your package
The ```__init__.py``` module should import the ```Birds``` and ```Mammals``` class from the two modules.
```
from .mammals import Mammals
from .birds import Birds
from .fish import Fish
```

#### d. Test your animals package
Using a python script or an interactive python session outside the package, test your brand new package:

```
import animals

m = animals.Mammals()
m.printMembers()

b = animals.Birds()
b.printMembers()
```

#### e. Add another module called ```fish.py``` amd integrate it into your package

#### f. Reorganize your package such that you can use it like this:
```
import animals

harmless_birds = animals.harmless.Birds()
harmless_birds.printMembers()

dangerous_fish = animals.dangerous.Fish()
dangerous_fish.printMembers()
```
```
#I created two new packages within the package and removed the dangerous or
#harmless from each list
import animals
import animals.harmless
import animals.dangerous

m = animals.Mammals()
m.printMembers()

b = animals.Birds()
b.printMembers()

f = animals.Fish()
f.printMembers()

hb = animals.harmless.Birds()
hb.printMembers()

dm = animals.dangerous.Mammals()
dm.printMembers()

```
## 2. Debugging
Investigate buggy code using the *pdb* or *ipdb* debugger. Have a look at slides 27-41 of this mornings's session for help.

#### a. Find all the bugs in the dicegame
Clone this repo (if you have not already done so), go to ```buggy```  and run the ```main.py``` with a debug tracer added to the code. Once you have fixed all errors, the game should correctly add up the values of the dice for 6 consecutive turns.
```
#I changed from 1 to die.value on row 19 as the games should calculate the value #of the dices not the amount of dices…
#I changed from input() to raw_input() on row 58, perhaps was this due to python #2/3 version problems
#
#I removed the i_just_throw_an_exception and changed it to exit()
#
#I made sure that the count worked at row 42. c+1 instead of c

from .die import Die
#from .utils import i_just_throw_an_exception

class GameRunner:

    def __init__(self):
        self.dice = Die.create_dice(5)
        self.reset()

    def reset(self):
        self.round = 1
        self.wins = 0
        self.loses = 0

    def answer(self):
        total = 0
        for die in self.dice:
            #need to calc the numbers on the dice not the rounds, changed 
            #from 1 to below
            total += die.value
        return total

    @classmethod
    def run(cls):
        # Probably counts wins or something.
        # Great variable name, 10/10.
        c = 0
        while True:
            runner = cls()

            print("Round {}\n".format(runner.round))

            for die in runner.dice:
                print(die.show())

            guess = input("Sigh. What is your guess?: ")
            guess = int(guess)

            if guess == runner.answer():
                print("Congrats, you can add like a 5 year old...")
                runner.wins += 1
                #c+1 instead of 1
                c += c+1
            else:
                print("Sorry that's wrong")
                print("The answer is: {}".format(runner.answer()))
                print("Like seriously, how could you mess that up")
                runner.loses += 1
                c = 0
            print("Wins: {} Loses {}".format(runner.wins, runner.loses))
            runner.round += 1

            if c == 6:
                print("You won... Congrats...")
                print("The fact it took you so long is pretty sad")
                break
            
            #perhaps this was a python 2 or 3 issue, when I changed to 
            #raw_input it worked
            prompt = raw_input('Would you like to play again?[Y/n]: ')
            print(prompt)

            if prompt == 'Y' or prompt == '':
                continue
                
            else:
                #added an exit() here instead
                exit()
```
#### b. If you cannot get enough of debugging
Ask your neighbour to introduce more bugs into the above (or any other) code examples and try to find the bug using the debugger. 

## 3. Profiling
In this section, you should get more familiar with code profiling, in particular with the tools ```cProfile```, ```line_profiler``` and ```memory_profiler```. Have a look at slides 44-52 from this morning's session to understand what they are doing and when you should use them. Try out profiling both from the command line and using interactive python (e.g. jupyter notebook).

#### a. Investigate the performance of the ```matmult.py``` script
In which line(s) of the script would you start optimizing for speed? Which line(s) create the most memory?
```
The two lines that create the list use the most time. This would probably be the best places to start. To do this I needed to make parts of the script into functions, otherwise the kernprof function would not work.
```
#### b. Investigate the performance of the ```euler72.py``` script
In which line(s) of the script would you start optimizing for speed? Which line(s) create the most memory?
(This is one problem from the euler project: [https://projecteuler.net/problem=72](https://projecteuler.net/problem=72))
```
Line 26 takes along time, perhaps that is a good start
```
#### c. Improve the performance of the ```matmult.py``` script
What is the best performance that you achieved with N=250?
```
I could not come up with an idea to improve it
```
