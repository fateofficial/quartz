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


# Exercise 3
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

```tikz
\begin{axis}[
    xlabel={Element Position in List},
    ylabel={Time Taken (s)},
    legend pos=north west,
    grid=both,
]
    % Linear Search
    \addplot coordinates {
        (7, 0.015) 
        (899, 2.055)
        (3000, 6.625)
        (8991, 19.846)
    };
    \addlegendentry{Linear Search}

    % Binary Search
    \addplot coordinates {
        (7, 0.078) 
        (899, 0.063)
        (3000, 0.079)
        (8991, 0.062)
    };
    \addlegendentry{Binary Search}
\end{axis}
```
