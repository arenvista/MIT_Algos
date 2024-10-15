# Table of Contents
<!-- vim-markdown-toc Redcarpet -->

* [Sets and Sorting](#sets-and-sorting)
    * [Set Interface](#set-interface)
    * [How to implement a set?](#how-to-implement-a-set)
        * [Unordered Array](#unordered-array)
        * [Storing by Key](#storing-by-key)
            * [Permutation Sort](#permutation-sort)
            * [Selection Sort](#selection-sort)
                * [Example](#example)

<!-- vim-markdown-toc -->
# Sets and Sorting
## Set Interface

| Type      | Method                                                                               | Def.                                                                                                                                                                                                                                                                      |
|-----------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Container | build(A) <br> len() </br>                                                            | Given an iterable A, build sequence from items in A return the number of stored items                                                                                                                                                                                     |
| Static    | find(k)                                                                              | return the sorted item with key k                                                                                                                                                                                                                                         |
| Dynamic   | insert(k)  <br> delete()<br>                                                         | add x to set ()<br> remove and return the stored item with key k <br>                                                                                                                                                                                                     |
| Order     | iter_ord () <br> find_min() <br> find_max() <br> find_next(k) <br> find_prev(k) <br> | return the stored items one-by-one in key order<br>return the stored item with smallest key<br> returned the stored item with largest key<br>return the stored item with smallest key larger than k<br>returned the stored item with largest key smaller than k<br> |

Question: What exactly is insert() doing?

Answer: x is the object that contains all the information and there exists a key (k). Insert(k) takes x and associates it with k

## How to implement a set?
### Unordered Array

One way to implement a set is to just store a giant array of objects that are in the set

`[x1] [x2] [x3] [...] [ ] [xn]`

*How can we implement this is the set is unordered? Presume we want to know in a set of students if Erick is in the set.*
- We can loop through each value in the set and test each x<sub>i</sub> if the value = Erick

`[x1] [x2] [x3] [...] [ ] [Erick]`
- 0(n); in the worst case Erick is the last person in the set

This is all to say it is possible to create a set using an unordered array, given this is going to take a lot of time to search 

<table>
    <tr>
        <th rowspan="2">Data Structure</th>
        <th colspan="5">Operations</th>
    </tr>
    <tr>
        <th>Container</td>
        <th>Static</td>
        <th colspan="3">Order</td>
    </tr>
        <td></td>
        <td>build(A)</td>
        <td>find(k)</td>
        <td>insert(x)<br>delete(k)</td>
        <td>find_min()<br>find_max()</td>
        <td>find_prev(k)<br>find_next(k)</td>
    <tr>
    <tr>
        <td> Array </td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
    </tr>
</table>

### Storing by Key

Instead of an array of just names, consider if we instead had an array of *student id #s*
- where the A<sub>1</sub> is the smallest id # and A<sub>n</sub> is the largest id number; such that A<sub>n-1</sub> < A<sub>n</sub>

This lets us optimize for some implementations at the cost of a longer runtime when building the inital set

<table>
    <tr>
        <th rowspan="2">Data Structure</th>
        <th colspan="5">Operations</th>
    </tr>
    <tr>
        <th>Container</td>
        <th>Static</td>
        <th colspan="3">Order</td>
    </tr>
        <td></td>
        <td>build(A)</td>
        <td>find(k)</td>
        <td>insert(x)<br>delete(k)</td>
        <td>find_min()<br>find_max()</td>
        <td>find_prev(k)<br>find_next(k)</td>
    <tr>
    <tr>
        <td> Array </td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
        <td>n</td>
    </tr>
    <tr>
        <td>Sorted Array</td>
        <td>nlogn</td>
        <td>log n</td>
        <td>n</td>
        <td>1</td>
        <td>log n</td>
    </tr>
</table>

Now finding the min/max is way faster - just look at the ends since the arrays are already sorted

Also since the array is already sorted we can implement *binary search* which is akin to traversing a binary tree where the search time is 0(log n)

*But how do we get a sorted array?*

Note:
- Input: Array<sub>A</sub> of n numbers/keys
- Output: Sorted Array<sub>B</sub>

Volcabulary:
* Destructive: Overwrites the input array
* In place: Uses O(1) extra place

#### Permutation Sort

By def. a sorted array is some permutation of an unsorted array. (it's the same componets just in sorted order)

Then we could search through all permutations and when we find one that's sorted return the value

```python
def permutation_sort(A):
    for B in permutations(A):
        if is_sorted(B):
            return B
```

Steps:

Recall: Omega is the minimum time (best-case)
1. Enumerate permutations: $\Omega$(n!)
2. Check if permutation is sorted $\theta$(n)
 ```python
for i in range(len(A)-1):
    if B[i] >= B[i+1]:
        return False
return True
 ```
So to do permutation sort would have a runtime of $\Omega$(n!*n)

#### Selection Sort

##### Example 

Say we want to sort this list of numbers:
```
8 2 4 9 3
```

Find largest number 

```
8 2 4 9 3
      *
```
Stick it to the end
```
8 2 4 3 | 9 
          *
```
Now by induction we can say everything to the right of | is in sorted order

We can then look to the left of the | and repeat, find the largest item
```
8 2 4 3 | 9 
*         
```
And move it to the back and repeat
```
2 4 3 | 9 8
          *
```

Steps:
1. Found the index with biggest number  w index $\leq$ 1
2. Swap into place
3. Sort from index 1 to i-1

*Helper Function for Selection Sort*
```python
def prefix_max(A, i):
    """ Retrn index of maximum in A[i:+1]"""
    if i>0:
        j = prefix_max(A, i-1)
        if A[i] < A[j]:
            return j
    return i
```
Largest element 0, ..., i 
1. Either it's at index i 
2. Or has index < i

32:24
