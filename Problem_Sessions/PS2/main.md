ntroduction to Algorithms: 6.006
^rassachusetts Institute of Technology

Instructors: Erik Demaine, Jason Ku, and Justin Solomon Problem Session 2

Problem Session 2

## Problem 1-1. Solving recurrences

Derive solutions to the following recurrences in two ways: via a recursion tree and via Master

Theorem. A solution should include the tightest upper and lower bounds that the recurrence will

allow. Assume T (1) ∈ Θ(1).

√

(a) T (n) = 2 T (n

2 ) + O( n)

√

(b) T (n) = 8 T (n

4 ) + O(n n)

(c) T (n) = T (n

3 ) + T (n

4 ) + Θ(n) assuming T (a) < T (b) for all a < b

## Problem 1-2. Stone Searching

Sanos is a supervillain on an intergalactic quest in search of an ancient and powerful artifact called
the Thoul Stone. Unfortunately she has no idea what planet the stone is on.
- The universe is composed of an infinite number of planets, each identified by a unique positive integer. 
    - n = # of planets
- On each planet is an oracle who, after some persuasion, will tell Sanos whether or not the Thoul Stone is on a planet having a strictly higher planet identifier than their own.
    - return if k(target) $\leq$ n
- Interviewing every oracle in the universe would take forever, and Sanos wants to find the Thoul Stone quickly. 

Supposing the Thoul Stone resides on planet k, describe an algorithm to help Sanos find the Thoul Stone by
interviewing at most O(log k) oracles.

---
This is suggesting binary search. This has 0(logn) runtime:
- Start in the middle, determine if at the point 
    - If not determine if top half or bottom half
- Search respective half (top/bottom) by checking the value at it's center 
    - Repeat if the ceneter is not = k; reduce the space to search to (center, top) | (bottom, ceneter)

## Problem 1-3. Collage Collating

Fodoby is a company that makes customized software tools for creative people. Their newest software, Ottoshop, helps users make collages by allowing them to overlay images on top of each other in a single document.

Describe a database to keep track of the images in a given document

Which supports the following operations:
1. make document(): construct an empty document containing no images
2. import image(x): add an image with unique integer ID x to the top of the document
3. display(): return an array of the document’s image IDs in order from bottom to top
4. move below(x, y): move the image with ID x directly below the image with ID y

* Operation (1) should run in worst-case O(1) time
* Operations (2) and (3) should each run in worst- case O(n) time
* Operation (4) should run in worst-case O(log n) time, where n is the number of images contained in a document at the time of the operation.
---


## Problem Session 2

## Problem 1-4. Brick Blowing

Porkland is a community of pigs who live in n houses lined up along one side of a long, straight

street running east to west. Every house in Porkland was built from straw and bricks, but some

houses were built with more bricks than others. One day, a wolf arrives in Porkland and all the

pigs run inside their homes to hide. Unfortunately for the pigs, this wolf is extremely skilled at

blowing down pig houses, aided by a strong wind already blowing from west to east. If the wolf

blows in an easterly direction on a house containing b bricks, that house will fall down, along with

every house east of it containing strictly fewer than b bricks. For every house in Porkland, the wolf

wants to know its damage, i.e., the number of houses that would fall were he to blow on it in an

easterly direction.

(a) Suppose n = 10 and the number of bricks in each house in Porkland from west to east

is [34, 57, 70, 19, 48, 2, 94, 7, 63, 75]. Compute for this instance the

damage for every house in Porkland.

(b) A house in Porkland is special if it either (1) has no easterly neighbor or (2) its adja-

cent neighbor to the east contains at least as many bricks as it does. Given an array

containing the number of bricks in each house of Porkland, describe an O(n)-time

algorithm to return the damage for every house in Porkland when all but one house

in Porkland is special.

(c) Given an array containing the number of bricks in each house of Porkland, describe

an O(n log n)-time algorithm to return the damage for every house in Porkland.

(d) Write a Python function get damages that implements your algorithm.

1 def get_damages(H):

’’’2

3 Input: H | list of bricks per house from west to east

4 Output: D | list of damage per house from west to east

’’’5

6 D = [1 for _ in H]

7 ##################

8 # YOUR CODE HERE #

9 ##################

10 return D

^rIT OpenCourseWare

https://ocw.mit.edu

6.006 Introduction to Algorithms

Spring 2020

For information about citing these materials or our Terms of Use, visit: https://ocw.mit.edu/terms
