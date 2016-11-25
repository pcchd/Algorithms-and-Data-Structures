# Lecture 1


## Peak Finding


### One Dimensional

-   A position `b` in array of `a, b, c, d, e, f` is a peak iff `b >= a` and `b >= c`
    For edges (`f`) we only look at one side.

1.  Problem: Find a peak if it exists

    We have an array `a` of length `n`

    1.  Straightforward algorithm

        -   Start from the left, keep comparing until a peak is found
            Worst case complexity: `theta n`

    2.  Divide and Conquer Algorithm

        -   Start at `n/2`
        -   if `a[n/2] < a[n/2 - 1]` then only loot at left half `1 .. n/2 -1`
        -   else if `a[n/2] < a[n/2 + 1]` then only loot at right half `n/2 + 1 .. n`
        -   else `n/2` is a peak

            Complexity is `theta(log2 n)`


### Two Dimensional

-   An element `a` which is surrounded by `c` (top), `d` (right), `e` bottom and `b` (left), is a peak iff `a >= b, a >= d, a >= c, a >= e`

1.  Problem: Find peak if it exists

    We have a 2 dimensional array of `n X m` rows and columns

    1.  Greedy Ascent Algorithm

        -   Complexity: `theta(nm)`

    2.  Divide and Conquer: Incorrect approach

        -   Pick the middle column `j = m/2`
        -   Find a one-dimensional-peak at `(i, j)`
        -   Use `(i, j)` as a start to find one-dimensional peak on row `i`

        1.  Problem

            -   A 2D array might not have a peak

    3.  Divide and Conquer: Correct approach

        -   Pick a middle column `j = m/2`
        -   Find global maximum on column `j` at `(i, j)`
        -   Compare `(i, j-1), (i, j), (i, j + 1)`
        -   Pick left cols if `(i, j -1) > (i, j)`; Similarly for the right
        -   If `(i, j) >= (i, j-1), (i, j+1)`, then `(i, j)` is a 2-D peakq


### homework  Question

-   Argue that: every array has a peak


## Prerequisites


### Asymptotic complexity

-   Provide basic vocabulary for discussing design and analysis of algorithms
-   Allow suppressing useless (from POV of algorithm design) details like architecture/language/compiler
-   Allow making useful comparisons b/w different algorithms
-   Suppress constant factors and lower-order terms

1.  Big Oh

    -   Worst case running time of an algorithm
    -   Eventually for all sufficiently large `n`, `T(n)` is bounded above by a constant multiple of `f(n)`

2.  Omega

    -   Best case running time of an algorithm

3.  Theta

    -   Average case running time of an algorithm
    -   It is not the average of all times, but a function which represents all the times


# Lecture 2

-   An algorithms is computational proceduer for solving a problem

    input -> algorithm -> Output


## Model of computation

-   specifies
    -   what operations an algorithm is allowed
    -   cost (time, &#x2026;) of each operation
-   Can be considered different ways of thinking, similar to different programming styles (OOP, Functional etc)


### Random Access Machine

-   Mathematical analog of Random Access Memory
-   Random Access Memory is modeled by a big array, and is organized by **words**
-   A **word** is: `w` bits

1.  How we compute with this model?

    In constant time an algorithm can

    -   load a constant number of words in memory
    -   do a constant number of computations on them
    -   store a constant number of words


### Pointer Machine

-   Dynamically allocated objects
-   object: has a constant number of fields
-   field: is either a word (e.g int), or a pointer
-   pointer is something that points to another object, or has a special value `null`


## Cost Model of Python

-   List
    -   list = array
    -   object with constant number of attributes take constant time to manipulate
    -   list.append(x)
        -   table doubling (in lecture 9), takes constant time `O(1)`
    -   list = list1 + list
        -   Python simply create an empty list, and append each item of other two lists
        -   Since `list.append` is constant time operation, adding two lists is `1 + O(len list1) + O(len list2)` (<sub>1</sub> +\_ because for creating a new list)
    -   list.sort
        -   takes `O(|l| log |l|)` time
        -   uses comparison sort
-   Dict
    -   Dict[key] = value
        takes `O(1)` time
    -   A dict in python is a hash
    -   Most (not all) operations on dict are constant time


## Document distance problem

`d(D1, D2)`

-   Determine how different or similar two documents are
-   A document is a sequence of words. Can also be thought of as a string
-   A word is a string of alphanumeric characters


### Solutions

1.  Simple solution: Shared Words

    -   Split the document into words
    -   Compute word frequencies
    -   Compute the dot product of two vectors obtained from frequencies


## Recitation


### Document Distance

-   We have two strings

1.  Algorithm

    -   Split the lists into words, get rid of punctuation and lowercase every word
    -   Convert lists to vectors of word and frequency of the word in the list.
        i.e create frequency distribution of words in lists
    -   Find dot product of two vectors
        Dot product is simply multiplying the frequencies of same words from both vectors, and adding the results.
        If a word occur in only one vector, it contributes `0` to the sum.


### Python Cost Model
-- TODO
