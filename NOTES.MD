<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgb060d56">1. Lecture 1</a>
<ul>
<li><a href="#orgae2218c">1.1. Peak Finding</a>
<ul>
<li><a href="#org4856a4b">1.1.1. One Dimensional</a></li>
<li><a href="#orgfe7c30d">1.1.2. Two Dimensional</a></li>
<li><a href="#org5c302bf">1.1.3. homework  Question</a></li>
</ul>
</li>
<li><a href="#org3e3273d">1.2. Prerequisites</a>
<ul>
<li><a href="#org106908c">1.2.1. Asymptotic complexity</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgd58194b">2. Lecture 2</a>
<ul>
<li><a href="#org0dcc70e">2.1. Model of computation</a>
<ul>
<li><a href="#orgd7eb837">2.1.1. Random Access Machine</a></li>
<li><a href="#org6c5f025">2.1.2. Pointer Machine</a></li>
</ul>
</li>
<li><a href="#org4090c80">2.2. Cost Model of Python</a></li>
<li><a href="#org420014f">2.3. Document distance problem</a>
<ul>
<li><a href="#org81a1958">2.3.1. Solutions</a></li>
</ul>
</li>
<li><a href="#orgd22981c">2.4. Recitation</a>
<ul>
<li><a href="#org69f226e">2.4.1. Document Distance</a></li>
<li><a href="#org89dec41">2.4.2. Python Cost Model</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#orgf0491f1">3. Lecture 3</a>
<ul>
<li><a href="#org182ca27">3.1. Sorting</a>
<ul>
<li><a href="#orgc2da0d0">3.1.1. Insertion sort</a></li>
<li><a href="#org601f3e7">3.1.2. Binary-Insertion sort</a></li>
<li><a href="#orgc99957b">3.1.3. Merge Sort</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
</div>
\#HTML<sub>MATHJAX</sub>: path: <https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML>


<a id="orgb060d56"></a>

# Lecture 1


<a id="orgae2218c"></a>

## Peak Finding


<a id="org4856a4b"></a>

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


<a id="orgfe7c30d"></a>

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


<a id="org5c302bf"></a>

### homework  Question

-   Argue that: every array has a peak


<a id="org3e3273d"></a>

## Prerequisites


<a id="org106908c"></a>

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


<a id="orgd58194b"></a>

# Lecture 2

-   An algorithms is computational proceduer for solving a problem

    input -> algorithm -> Output


<a id="org0dcc70e"></a>

## Model of computation

-   specifies
    -   what operations an algorithm is allowed
    -   cost (time, &#x2026;) of each operation
-   Can be considered different ways of thinking, similar to different programming styles (OOP, Functional etc)


<a id="orgd7eb837"></a>

### Random Access Machine

-   Mathematical analog of Random Access Memory
-   Random Access Memory is modeled by a big array, and is organized by **words**
-   A **word** is: `w` bits

1.  How we compute with this model?

    In constant time an algorithm can

    -   load a constant number of words in memory
    -   do a constant number of computations on them
    -   store a constant number of words


<a id="org6c5f025"></a>

### Pointer Machine

-   Dynamically allocated objects
-   object: has a constant number of fields
-   field: is either a word (e.g int), or a pointer
-   pointer is something that points to another object, or has a special value `null`


<a id="org4090c80"></a>

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
        -   takes `O(|l| \log |l|)` time
        -   uses comparison sort
-   Dict
    -   Dict[key] = value
        takes `O(1)` time
    -   A dict in python is a hash
    -   Most (not all) operations on dict are constant time


<a id="org420014f"></a>

## Document distance problem

`d(D1, D2)`

-   Determine how different or similar two documents are
-   A document is a sequence of words. Can also be thought of as a string
-   A word is a string of alphanumeric characters


<a id="org81a1958"></a>

### Solutions

1.  Simple solution: Shared Words

    -   Split the document into words
    -   Compute word frequencies
    -   Compute the dot product of two vectors obtained from frequencies


<a id="orgd22981c"></a>

## Recitation


<a id="org69f226e"></a>

### Document Distance

-   We have two strings

1.  Algorithm

    -   Split the lists into words, get rid of punctuation and lowercase every word
    -   Convert lists to vectors of word and frequency of the word in the list.
        i.e create frequency distribution of words in lists
    -   Find dot product of two vectors
        Dot product is simply multiplying the frequencies of same words from both vectors, and adding the results.
        If a word occur in only one vector, it contributes `0` to the sum.


<a id="org89dec41"></a>

### Python Cost Model


<a id="orgf0491f1"></a>

# Lecture 3


<a id="org182ca27"></a>

## Sorting


<a id="orgc2da0d0"></a>

### Insertion sort

we have an array `[1, 4, 5, 2, 3 ... n]`

-   we start with considering item at second position to be a `key`, and swap it with the item left if it is greater then `key`
-   next we consider item at 3rd position as our key, and compare it with item on its left, and swap if needed; and do it repeatedly until it reaches its right place.
    i.e item on its left is less than `key`
-   same step is followed for every item until there are no more items left i.e until the array is sorted

-   **Complexity**

    \[T(n) = \theta(n^2)\]

    \(\theta(n)\) for compares and \(\theta(n)\) for swaps


<a id="org601f3e7"></a>

### Binary-Insertion sort

-   Same as insertion sort except instead of swapping, we use binary search to insert item in sorted part of the array (part left to `key`)
-   **Complexity**

    \[T(n) = \theta(n \log n)\]

    \(\theta(n)\) for compares, and \(\theta(\log n)\) for binary-searched insertions. This is assuming that insertion is \(\theta n\).
    If insertion involves shifting items to right (as with swapping), then the complexity is again $&theta; n<sup>2</sup>$b


<a id="orgc99957b"></a>

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
