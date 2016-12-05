<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgd3f73b2">1. Lecture 1</a>
<ul>
<li><a href="#org0f2b19e">1.1. Peak Finding</a>
<ul>
<li><a href="#org003d40b">1.1.1. One Dimensional</a></li>
<li><a href="#orgc09d629">1.1.2. Two Dimensional</a></li>
<li><a href="#orgceaefb8">1.1.3. homework  Question</a></li>
</ul>
</li>
<li><a href="#orgefde854">1.2. Prerequisites</a>
<ul>
<li><a href="#org426ed5a">1.2.1. Asymptotic complexity</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#org34e8887">2. Lecture 2</a>
<ul>
<li><a href="#org4f5c373">2.1. Model of computation</a>
<ul>
<li><a href="#orgb81e5df">2.1.1. Random Access Machine</a></li>
<li><a href="#org2f38463">2.1.2. Pointer Machine</a></li>
</ul>
</li>
<li><a href="#orgfb303ef">2.2. Cost Model of Python</a></li>
<li><a href="#orgb52ad0b">2.3. Document distance problem</a>
<ul>
<li><a href="#org13e2e6c">2.3.1. Solutions</a></li>
</ul>
</li>
<li><a href="#org0d1d4d9">2.4. Recitation</a>
<ul>
<li><a href="#orgb4f61fe">2.4.1. Document Distance</a></li>
<li><a href="#org9726687">2.4.2. Python Cost Model</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#org46250b4">3. Lecture 3</a>
<ul>
<li><a href="#orgd317ba8">3.1. Sorting</a>
<ul>
<li><a href="#orgb688642">3.1.1. Insertion sort</a></li>
<li><a href="#orgda92ecd">3.1.2. Binary-Insertion sort</a></li>
<li><a href="#org686bc62">3.1.3. Merge Sort</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgc6bea29">4. Lecture 4</a>
<ul>
<li><a href="#orged62f0e">4.1. Priority Queue</a>
<ul>
<li><a href="#orgc7480fc">4.1.1. Operations allowed on Priority Queue</a></li>
</ul>
</li>
<li><a href="#org3eeb3be">4.2. Heap</a></li>
<li><a href="#org13f46b6">4.3. Heap Sort</a></li>
</ul>
</li>
</ul>
</div>
</div>


<a id="orgd3f73b2"></a>

# Lecture 1


<a id="org0f2b19e"></a>

## Peak Finding


<a id="org003d40b"></a>

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


<a id="orgc09d629"></a>

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


<a id="orgceaefb8"></a>

### homework  Question

-   Argue that: every array has a peak


<a id="orgefde854"></a>

## Prerequisites


<a id="org426ed5a"></a>

### Asymptotic complexity

-   Provide basic vocabulary for discussing design and analysis of algorithms
-   Allow suppressing useless (from POV of algorithm design) details like architecture/language/compiler
-   Allow making useful comparisons b/w different algorithms
-   Suppress constant factors and lower-order terms

1.  Big Oh

    -   Worst case running time of an algorithm
    -   Eventually for all sufficiently large `n`, `T(n)` is bounded above by a constant multiple of `f(n)`

    1.  Properties

        -   If \(f(x)\) can be written as a finite set of sum of other functions, then the fastest growing function determine the order of \(f(n)\)

            e.g \[f(n) = 9 log n + 5(log n)^3 + 3n^2 + 2n^3 = O(n^3)\]

        -   Normally we ignore when variable is being multiplied with a constant, however in case of \(k^{nc}\) where \(n\) is variable and \(c\) is constant, we cannot ignore \(c\). It contributes exponentially, and is hence significant

        -   \(O(c^n)\) and \(O(n^c)\) are very different. For \(c > 1\), \(O(c^n)\) grows much faster than \(O(n^c)\)
        -   A function that grows faster than \(n^c\) for any \(c\) is called *superpolynomial*.
        -   A function that grows slowly than any exponential function \(c^n\) is called *subexponential*
        -   We may ignore all powers of \(n\) inside of logarithms.
            \(O(log n)\) is same as \(O(log (n^c))\) because \(log(n^c) = c log n\)
        -   logs with different bases are equivalent

        -   **Product**

            \[f_1 = O(g_1) \text{ and } f_2 = O(g_2) \Rightarrow f_1 f_2 = O(g_1 g_2)\]

            \[f.O(g) = O(fg)\]

        -   **Sum**

            \[f_1 = O(g_1) \text{ and } f_2 = O(g_2) \Rightarrow f_1 + f_2 = O(|g_1| + |g_2|)\]

        -   **Multiplication by a constant**

            For a constant \(k\), \(O(kg) = O(g)\) if \(k\) is nonzero

        -   **Orders of common functions**

            <table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


            <colgroup>
            <col  class="org-left" />

            <col  class="org-left" />
            </colgroup>
            <thead>
            <tr>
            <th scope="col" class="org-left">Notation</th>
            <th scope="col" class="org-left">Name</th>
            </tr>
            </thead>

            <tbody>
            <tr>
            <td class="org-left">\(O(1)\)</td>
            <td class="org-left">constant</td>
            </tr>


            <tr>
            <td class="org-left">\(O(\log \log n)\)</td>
            <td class="org-left">double logarithmic</td>
            </tr>


            <tr>
            <td class="org-left">\(O(\log n)\)</td>
            <td class="org-left">logarithmic</td>
            </tr>


            <tr>
            <td class="org-left">\(O((\log n)^{c}), c > 1\)</td>
            <td class="org-left">polylogarithmic</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n^{c}), 0 < c < 1\)</td>
            <td class="org-left">fractional power</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n)\)</td>
            <td class="org-left">linear</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n\log ^{*}n)\)</td>
            <td class="org-left">n log-star n</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n\log n)=O(\log n!)\)</td>
            <td class="org-left">linearithmic, loglinear, or quasilinear</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n^{2})\)</td>
            <td class="org-left">quadratic</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n^{c})\)</td>
            <td class="org-left">polynomial or algebraic</td>
            </tr>


            <tr>
            <td class="org-left">\(O(c^{n}), c > 1\)</td>
            <td class="org-left">exponential</td>
            </tr>


            <tr>
            <td class="org-left">\(O(n!)\)</td>
            <td class="org-left">factorial</td>
            </tr>
            </tbody>
            </table>

2.  Omega

    -   Best case running time of an algorithm

3.  Theta

    -   Average case running time of an algorithm
    -   It is not the average of all times, but a function which represents all the times


<a id="org34e8887"></a>

# Lecture 2

-   An algorithms is computational proceduer for solving a problem

    input -> algorithm -> Output


<a id="org4f5c373"></a>

## Model of computation

-   specifies
    -   what operations an algorithm is allowed
    -   cost (time, &#x2026;) of each operation
-   Can be considered different ways of thinking, similar to different programming styles (OOP, Functional etc)


<a id="orgb81e5df"></a>

### Random Access Machine

-   Mathematical analog of Random Access Memory
-   Random Access Memory is modeled by a big array, and is organized by **words**
-   A **word** is: `w` bits

1.  How we compute with this model?

    In constant time an algorithm can

    -   load a constant number of words in memory
    -   do a constant number of computations on them
    -   store a constant number of words


<a id="org2f38463"></a>

### Pointer Machine

-   Dynamically allocated objects
-   object: has a constant number of fields
-   field: is either a word (e.g int), or a pointer
-   pointer is something that points to another object, or has a special value `null`


<a id="orgfb303ef"></a>

## Cost Model of Python

-   List
    -   list = array
    -   object with constant number of attributes take constant time to manipulate
    -   list.append(x)
        -   table doubling (in lecture 9), takes constant time `O(1)`
    -   list = list1 + list
        -   Python simply create an empty list, and append each item of other two lists
        -   Since `list.append` is constant time operation, adding two lists is `1 + O(len list1) + O(len list2)` (\_1 +\_ because for creating a new list)
    -   list.sort
        -   takes `O(|l| \log |l|)` time
        -   uses comparison sort
-   Dict
    -   Dict[key] = value
        takes `O(1)` time
    -   A dict in python is a hash
    -   Most (not all) operations on dict are constant time


<a id="orgb52ad0b"></a>

## Document distance problem

`d(D1, D2)`

-   Determine how different or similar two documents are
-   A document is a sequence of words. Can also be thought of as a string
-   A word is a string of alphanumeric characters


<a id="org13e2e6c"></a>

### Solutions

1.  Simple solution: Shared Words

    -   Split the document into words
    -   Compute word frequencies
    -   Compute the dot product of two vectors obtained from frequencies


<a id="org0d1d4d9"></a>

## Recitation


<a id="orgb4f61fe"></a>

### Document Distance

-   We have two strings

1.  Algorithm

    -   Split the lists into words, get rid of punctuation and lowercase every word
    -   Convert lists to vectors of word and frequency of the word in the list.
        i.e create frequency distribution of words in lists
    -   Find dot product of two vectors
        Dot product is simply multiplying the frequencies of same words from both vectors, and adding the results.
        If a word occur in only one vector, it contributes `0` to the sum.


<a id="org9726687"></a>

### Python Cost Model


<a id="org46250b4"></a>

# Lecture 3


<a id="orgd317ba8"></a>

## Sorting


<a id="orgb688642"></a>

### Insertion sort

we have an array `[1, 4, 5, 2, 3 ... n]`

-   we start with considering item at second position to be a `key`, and swap it with the item left if it is greater then `key`
-   next we consider item at 3rd position as our key, and compare it with item on its left, and swap if needed; and do it repeatedly until it reaches its right place.
    i.e item on its left is less than `key`
-   same step is followed for every item until there are no more items left i.e until the array is sorted

-   **Complexity**

    \[T(n) = \theta(n^2)\]

    \(\theta(n)\) for compares and \(\theta(n)\) for swaps


<a id="orgda92ecd"></a>

### Binary-Insertion sort

-   Same as insertion sort except instead of swapping, we use binary search to insert item in sorted part of the array (part left to `key`)
-   **Complexity**

    \[T(n) = \theta(n \log n)\]

    \(\theta(n)\) for compares, and \(\theta(\log n)\) for binary-searched insertions. This is assuming that insertion is \(\theta n\).
    If insertion involves shifting items to right (as with swapping), then the complexity is again $&theta; n^2$b


<a id="org686bc62"></a>

### Merge Sort

-   We start with an array `A`; we split it into `L`  and `R`
-   We split `L` and `R` same way as `A`, until we have single item arrays
-   We **merge** arrays from bottom up, and we get the sorted array.
    Sorting work is done in the merge step
-   **Merge step**
    -   We start at the bottom, and merge two items while keeping smaller item first
    -   Same is done with all pairs, and we now have 2 item arrays at bottom
    -   Then we merge 2 item arrays
        -   We pick first item (smallest) of one (of the two) array, and compare it with first item on the other array
        -   We put smaller item first, and compare the same item with other item of second array until `second array item > first array item` is found
        -   Same is done with all the 2-item arrays, and we end up with 4 item arrays
    -   All arrays are merged in same fashion until we have only one array; which is the sorted array we wanted

-   **Complexity**

    \[T(n) = \theta n \log  n\]

-   Insertion sort has advantage over Merge Sort when auxiliary space is considered, because Insertion Sort works in-place


<a id="orgc6bea29"></a>

# Lecture 4


<a id="orged62f0e"></a>

## Priority Queue

Implements a set `S` of elements, and each of these elements is associated with a key


<a id="orgc7480fc"></a>

### Operations allowed on Priority Queue

-   **insert(S, x)**: Insert element `x` into set `S`
-   **max(S)**: Return element of `S` which the largest key
-   **extract\_max(S)**: Return element of `S` which the largest key, and remove it from `S`
-   **increase\_key(S, x, k)**: Increase the value of `x`'s key to new value `k`


<a id="org3eeb3be"></a>

## Heap

-   An implementation of Priority Queue

-   An array visualized as a nearly complete binary tree

    for example, if we have an array of 10 elements, we can number the array slots from 1 to 10 (irrespective of the contents of the slot),
    and visualize it as a binary tree.

    <table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


    <colgroup>
    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />

    <col  class="org-right" />
    </colgroup>
    <tbody>
    <tr>
    <td class="org-right">\(_1\)</td>
    <td class="org-right">\(_2\)</td>
    <td class="org-right">\(_3\)</td>
    <td class="org-right">\(_4\)</td>
    <td class="org-right">\(_5\)</td>
    <td class="org-right">\(_6\)</td>
    <td class="org-right">\(_7\)</td>
    <td class="org-right">\(_8\)</td>
    <td class="org-right">\(_9\)</td>
    <td class="org-right">\(_{10}\)</td>
    </tr>


    <tr>
    <td class="org-right">16</td>
    <td class="org-right">14</td>
    <td class="org-right">10</td>
    <td class="org-right">8</td>
    <td class="org-right">7</td>
    <td class="org-right">9</td>
    <td class="org-right">3</td>
    <td class="org-right">2</td>
    <td class="org-right">4</td>
    <td class="org-right">1</td>
    </tr>
    </tbody>
    </table>

                                 1
                               -----
                              ( 16  )
                               -----
                         _______/\_________
                        /                  \ 3
                     2 /                  -----
                   -----                 (  10 )
                  ( 14  )                 -----
                   -----\                6 /  \ 7
                    /    \          ----- /    \ -----
                 4 /    5 \        (  9  )      \  3  )
                -----    -----      -----        -----
               (  8  )  (  7  )
                -----    -----
                 / \  ----/ 10
                /   \(  1  )
             8 /   9 \-----
         -----/      -----
        (  2  )     (  4  )
         -----       -----

    -   **Heap as a tree**
        -   Root of the tree is the first element (\(i = 1\))
        -   \(parent(i) = \frac{i}{2}\)
        -   \(left(i) = 2i\)
        -   \(right(i) =  2i + 1\)

    -   **Max heap property**

        the key of a node is \(\geq\) the keys of its children

    -   Min heap property

        the key of a node is \(\leq\) the keys of its children

-   **Heap Operations**
    -   *build\_max\_heap* : produces a max heap from an arbitrary (unordered) array

    -   *max\_heapify*: correct a *single* violation of the heap property in a subtree's root

        Complexity of `max_heapify` is \(\lg{n}\) is because a heap is a nearly complete binary tree, so height of the tree is bounded by \(\lg{n}\),
        so every algorithm that goes level by level is \(\lg{n}\) complexity

    -   insert, extract\_max, heapsort

-   **max\_heapify**
    -   Assume that the trees rooted at `left(i)` and `right(i)` are max-heaps
    -   If element `A[i]` violates the max-heap property, correct violation by "trickling" element A[i] down the tree,
        making the subtree rooted at index i a max-heap

    -   Pseudo Code

            def max_heapify(A, largest):
              l = left(i)
              r = right(i)

              if l <= heap_size(A) and A[l] > A[i]:
                largest = l
              else:
                largets = i

              if r <= heap_size(A) and A[r] > A[largest]:
                largest = r

              if largest != i:
                exchange(A[i], A[largest])
                max_heapify(A, largest)

-   **build\_max\_heap(A)**

    Converting an array \(A[1..n]\) to a max-heap

        def build_max_heap(A):
          for i in reversed(range(1, n/2)):
            max_heapify(A, i)

    We start at `n/2` here because all `A[n/2 + 1 ... n]` elements are leaves, so we can safely start with the assumption that all the child nodes
    are max-heaps

    -   Complexity by simple analysis is \(O(n\log{n})\), but with proper analysis, it actually is \(\theta{n}\)

        Observe that

        1.  `max_heapify` takes constant time \(O(1)\) for nodes that are one level above leaves
            and in general \(O(l)\) time for nodes that are `l` levels above leaves

        2.  `n/4` nodes with level 1, `n/8` with level 2, &#x2026;. , 1 node with \(\log{n}\) level

        Total amount of work in the for loop can be summed as
        \[\frac{n}{4}(1.c) + \frac{n}{8} (2.c) + \frac{n}{16} (3.c) + ... + 1(\lg{n} c)\]

        Set \(n/4 = 2^k\)
        \[c.2^k(\frac{1}{2^0} + \frac{2}{2^1} + \frac{3}{2^2} + ... + \frac{(k+1)}{2^k})\]

        Here, \((\frac{1}{2^0} + \frac{2}{2^1} + \frac{3}{2^2} + ... + \frac{(k+1)}{2^k})\) is bounded by a constant \(\sum_{i=0}^k \frac{i+1}{2^i}\),
        and \(c\) is a constant, and \(2^k\) is actually `n\4`, so we have \(\theta{n}\) complexity


<a id="org13f46b6"></a>

## Heap Sort

Algorithm:

1.  `build_max_heap` from the unordered array
2.  Find max element `A[1]`
3.  Swap elements `A[n]` with `A[1]`

    now the maximum element is at the end of the array
4.  Discard node `n` from the heap simply by decrementing heap size
5.  New root may violate Max Heap Property but the children are max heaps. Run `max_heapify` to fix it
6.  Go to step 2 unless heap is empty

Complexity is \(O(n\log{n})\)

-   After `n` iterations, the heap is empty.
-   Every iteration involves a swap and a `max_heapify` operation which takes \(O(\log{n})\)
