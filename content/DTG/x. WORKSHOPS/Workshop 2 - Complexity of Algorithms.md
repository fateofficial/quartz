A search function takes as inputs a list $(a_0, \dots, a_{n-1})$ and an element $x$. The task is to find the element $x$ in the list if it is a member. More precisely, if there is an index $i$ such that $a_i = x$ then a search algorithm should return the index $i$. If there is no such index we want a return value of $-1$. We will restrict ourselves to lists of integers. If we denote by $A$ the set of all finite lists of integers then a search function is a map

![[Pasted image 20241228132247.png]]





# Exercise 1

## 1. 
Explain why f is not a function using the list (3, 4, 4, 5) as an example.
This is because of  the definition of a function:

A function $f$ from set $A$ (domain) to set $B$ (codomain) is a rule that assigns exactly one output in $B$ for each input from $A$. This means for each input $x$, there should be a single corresponding output $f(x)$.

In the list (3,4,4,5), the element 4 appears twice, at indices 1 and 2. If we try to search for 4 using this list, the search function could return either index 1, or index 2. This violates the rule that each input should have one and only one output, which is a fundamental property of functions.


## 2. 
If we require the lists we use to not have repeated elements, then $f$ can be seen as a function. Decide whether this function is injective, surjective or bijective.

Multiple values in domain give the same value in codomain which is -1. Therefore it is not injective.

Every value in the codomain is at least mapped by one in the codomain. because if list is from 1 to n amount, could have an index in the range of 0 to n-1, or -1 by not being the number looked for. Therefore it is surjective.


| **Injective**  | A function where every element in the domain maps to a unique element in the codomain (no two elements map to the same codomain element).                                     |     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| **Surjective** | A function where every element in the codomain is mapped to by at least one element in the domain.                                                                            |     |
| **Bijective**  | A function that is both injective and surjective, meaning every element in the domain maps to a unique element in the codomain, and every element in the codomain is covered. |     |


# Exercise 2
## 1.
Implement the two algorithms in the provided file SearchCompare.c.

```
int LinSearch(int array[], int x, int n){  
    int i=0;  
    while (i < n && x != array[i]) {  
        i++;  
    }  
    if (i<n) {  
        return i;  
    } else return -1;  
  
}
```

```
int BinSearch(int array[], int x, int n){  
    int i=0;  
    int j=n-1;  
    while (i<j) {  
        int m = (i+j)/2;  
        if (x>array[m]) {  
            i=m+1;  
        } else j = m;  
    }  
    if (x==array[i]) {  
        return i;  
    } else return -1;  
}
```

## 2.
Check if the element 7000 appears in the lists List500.txt, List1000.txt, List2000.txt, List6000.txt, and List9000.txt.
```
500 7000
The size of the list is 500
BinSearch needed: 0.0320000s
LinSearch needed: 1.1240000s
LinSearch: 7000 is not in the list
BinSearch: 7000 is not in the list

1000 7000
What number are we searching for?
The size of the list is 1000
BinSearch needed: 0.0470000s
LinSearch needed: 2.2630000s
LinSearch: 7000 is not in the list
BinSearch: 7000 is not in the list

2000 7000
What number are we searching for?
The size of the list is 2000
BinSearch needed: 0.0470000s
LinSearch needed: 4.3760000s
LinSearch: 7000 is not in the list
BinSearch: 7000 is not in the list

6000 7000
What number are we searching for?
The size of the list is 6000
BinSearch needed: 0.0470000s
LinSearch needed: 13.1610000s
LinSearch: 7000 is not in the list
BinSearch: 7000 is not in the list

9000 7000
The size of the list is 9000
BinSearch needed: 0.0470000s
LinSearch needed: 19.4500000s
LinSearch: 7000 is not in the list
BinSearch: 7000 is not in the list
```
## 3.
The elements 7, 899, 3000 and 8991 are all contained in the list List9000.txt. Compare how long the different algorithms need to find them.
```
search(9000,7);
BinSearch needed: 0.0590000s
LinSearch needed: 0.0090000s
LinSearch: 7 is in position 5
BinSearch: 7 is in position 5

search(9000,899);
BinSearch needed: 0.0640000s
LinSearch needed: 2.0840000s
LinSearch: 899 is in position 896
BinSearch: 899 is in position 896

search(9000,3000);
BinSearch needed: 0.0610000s
LinSearch needed: 6.7380000s
LinSearch: 3000 is in position 2990
BinSearch: 3000 is in position 2990

search(9000,8991);
The size of the list is 9000
BinSearch needed: 0.0600000s
LinSearch needed: 20.4520000s
LinSearch: 8991 is in position 8974
BinSearch: 8991 is in position 8974

```

## 4.
Take note of how long the algorithms take for the different lists and plot list size on the x-axis and the time it took on the y-axis.

For one million runs of bin bin search on a list with 9000, the time it takes is around 0.06 seconds.

For binary search however it drastically increases depending on the location and worst case ended up taking as much as circa 20.5 seconds.

![[Figure_1 1.png]]

# Exercise 2

## 1. 
Argue that the linear search algorithm will use 2n + 2 comparisons in the worst case. Describe the inputs for which this will happen.

**procedure:** LinearSearch($x$: element, $(a_0, a_1, \dots, a_{n-1})$: list)  
$i := 0$  
**while** $i < n \ \text{AND} \ x \neq a_i$:  
    $i := i + 1$  
**if** $i < n$:  
    **then return** $i$  
**else return** $-1$


Binary search checks the while loop which is a comparison 2n times because of the  **while** $i < n \ \text{AND} \ x \neq a_i$
So 2n comparisons are already made now the last 2 comparisons come for the closing iteration, the n+1 iteration.
Here the first comparison in the while loop fail and go directly to if statement, which is one comparison.
Then the closing if statement to check if a value is found is the last comparisons.
In total it is 2n+2 comparisons.


## 2.
Show that the number of comparisons in the worst case for linear search is in Θ(n).

To show that the number of comparisons in the worst case for linear search is in Θ(n)

Simplify Using $\Theta$-Notation Rules In $\Theta$-notation, constants and lower-order terms are ignored because we focus on the asymptotic growth rate Therefore: $$f(n) = 2n + 2 \quad \implies \quad f(n) \in \Theta(n)$$
The number of comparisons in the worst case for linear search grows linearly with $n$, so it is in $\Theta(n)$
## 3. 
Consider the binary search algorithm and assume that the list has length n = 2k .


**procedure:** BinarySearch($x$: element, $(a_0, a_1, \dots, a_{n-1})$: list)  
$i := 0$  
$j := n - 1$  
**while** $i < j$:  
    $m := \lfloor \frac{i + j}{2} \rfloor$  
    **if** $x > a_m$:  
        **then** $i := m + 1$  
    **else** $j := m$  
**if** $x = a_i$:  
    **then return** $i$  
**else return** $-1$