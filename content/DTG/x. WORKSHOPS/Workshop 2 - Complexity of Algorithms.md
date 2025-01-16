A search function takes as inputs a list $(a_0, \dots, a_{n-1})$ and an element $x$. The task is to find the element $x$ in the list if it is a member. More precisely, if there is an index $i$ such that $a_i = x$ then a search algorithm should return the index $i$. If there is no such index we want a return value of $-1$. We will restrict ourselves to lists of integers. If we denote by $A$ the set of all finite lists of integers then a search function is a map

![[Pasted image 20241228132247.png]]

The term **asymptotic** refers to the behavior of a function as its input approaches some limit, usually as n (typically the size of the input) becomes very large

| Notation | Meaning                                            | Description                                                                       |
| -------- | -------------------------------------------------- | --------------------------------------------------------------------------------- |
| Big O    | Upper bound (asymptotic upper limit)               | Function grows at most as fast as g(n)g(n)g(n), but it may grow at the same rate. |
| Small o  | Strict upper bound (asymptotic strict upper limit) | Function grows strictly slower than g(n)g(n)g(n); the ratio approaches zero.      |


| Notation  | Bound Type            | Definition                                     | Example                | Interpretation                          |
| --------- | --------------------- | ---------------------------------------------- | ---------------------- | --------------------------------------- |
| Big-O     | Upper bound           | $f(n) \leq c \cdot g(n)$ for large $n$         | $3n + 2 \in O(n)$      | $f(n)$ grows no faster than $g(n)$      |
| Big-Omega | Lower bound           | $f(n) \geq c \cdot g(n)$ for large $n$         | $n^2 \in \Omega(n)$    | $f(n)$ grows at least as fast as $g(n)$ |
| Big-Theta | Upper and Lower bound | $c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n)$ | $2n + 3 \in \Theta(n)$ | $f(n)$ grows exactly like $g(n)$        |






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

For one million runs of bin search on a list with 9000, the time it takes is around 0.06 seconds.

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

In the case of not found or last element:
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


#proof

Let $f(n)$ represent the number of comparisons in the worst case for linear search, where $n$ is the size of the input list. In the worst case, we perform $2n + 2$ comparisons:
$$
f(n) = 2n + 2
$$


To prove that $f(n) \in \Theta(n)$, we need to find constants $c_1$, $c_2$, and $n_0$ such that for all $n \geq n_0$, the following inequality holds:
$$
c_1 \cdot n \leq f(n) \leq c_2 \cdot n
$$


We want to show that $f(n) \leq c_2 \cdot n$ for some constant $c_2$. From $f(n) = 2n + 2$, we get:
$$
2n + 2 \leq c_2 \cdot n
$$
For large $n$, we can choose $c_2 = 4$, because:
$$
2n + 2 \leq 4n \quad \text{for all } n \geq 1
$$
Thus, the upper bound is satisfied with $c_2 = 4$.


Next, we want to show that $f(n) \geq c_1 \cdot n$ for some constant $c_1$. Again, using $f(n) = 2n + 2$, we get:
$$
2n + 2 \geq c_1 \cdot n
$$
This inequality holds for $c_1 = 2$, because:
$$
2n + 2 \geq 2n \quad \text{for all } n \geq 1
$$
Thus, the lower bound is satisfied with $c_1 = 2$.

We have shown that for sufficiently large $n$, say for $n \geq 1$, the function $f(n) = 2n + 2$ satisfies:
$$
2n \leq 2n + 2 \leq 4n
$$
Therefore, $f(n) \in \Theta(n)$, as required.


$\text{The number of comparisons in the worst case for linear search is in } \Theta(n).$



## 3. 

#algorithm 
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
Consider the binary search algorithm and assume that the list has length n = 2k .

### i)
Check that every full iteration of the while loop uses two comparisons.

In the while statement two comparisons are used.
$i < j$
For checking if search is finished,
$x > a_m$
Checks which side to discard, lower or higher values.

### ii)
Show that in the first iteration of the while loop $m = 2k^{- 1} - 1$
Assume the list has length $n = 2^k$.

1. Initialize: 
   - $i := 0$
   - $j := n - 1$

2. The middle index $m$ is calculated as:
   $$
   m = \left\lfloor \frac{i + j}{2} \right\rfloor = \left\lfloor \frac{n-1}{2} \right\rfloor
$$

3. Substituting $n = 2^k$:
   $$
   m = \left\lfloor \frac{2^k - 1}{2} \right\rfloor = \left\lfloor 2^{k-1} - \frac{1}{2} \right\rfloor 
$$

Because of the lower bounded brackets, it is rounded down to -1.

$$ \left\lfloor 2^{k-1} - \frac{1}{2} \right\rfloor = 2^{k-1} - 1
$$


Thus, in the first iteration, $m = 2^{k-1} - 1$.

### iii)
Argue that after the first time the while loop has run we have excluded half the elements of the list.

Because of the while loop in binary search, there are only two results of the main loop.
**while** $i < j$:  
    $m := \lfloor \frac{i + j}{2} \rfloor$  
    **if** $x > a_m$:  
        **then** $i := m + 1$  
    **else** $j := m$  

As seen m is the middle point it takes both the left pointer and right pointer and finds the middle ground.

If x the value searched for is bigger than list[m], which is the value of the middle index then discard the indexes that are lower, by setting i to m+1, which moves the lower pointer to middle index +1. However if x is not strictly  greater than then the upper pointer becomes m and therefore discard all higher values.


iv)
Check that we have to half the list $\log_2(n)$ times to end up with a list of just one element. (Remember that we assume $n = 2^k$.)

$$\log_2(n) = \log_2(2^k)$$ By applying the logarithmic identity $\log_b(x^m) = m \cdot \log_b(x)$, we get:
$$\log_2(2^k) = k \cdot \log_2(2)$$ Since $\log_2(2) = 1$, this simplifies to: 
$$\log_2(n) = k$$ Thus, the number of halvings required to reduce the list of size $n = 2^k$ to one element is $k$.

 This shows that it takes exactly $\log_2(n)$ halvings to reduce the list to one element, where $n$ is a power of 2. If $n$ is not a power of 2, the number of halvings will be approximately $\log_2(n)$, but there will be some rounding or fractional values since $\log_2(n)$ may not be an integer.

v)
Consider the final steps of the algorithm. Once $i = j$, the while loop checks its run condition once more. Then the algorithm continues to check if we have found the element in question. 
Show that the algorithm will need $2 \log_2(n) + 2$ comparisons.



while $i < j$:  
    $m := \lfloor \frac{i + j}{2} \rfloor$  
    **if** $x > a_m$:  
        **then** $i := m + 1$  
    **else** $j := m$  

Main loop contains two comparisons one in the while loop, and one in the if statement because it iterate log2(n) times, it does however fail after.


**if** $x = a_i$:  
    **then return** $i$  

When the for loop has ended and with the last comparison which is false this if statement is checked to see if element divided to is the element searched for, which is +1 comparisons.

The worst case of these iterations and amount of comparisons can be found  when taking the celing or floor of log2(n).

Total: $2\cdot \log_2(n)+2$ The amount of comparisons in the binary search implemented.


## 4. 
Show that the number of comparisons needed for binary search is $Θ(log2 (n))$.

#proof
Let $f(n)$ represent the total number of comparisons made by binary search. From our previous discussion, we know that binary search makes two comparisons per iteration in the main loop, and two final comparisons after the loop finishes. Therefore, the total number of comparisons is:

$$
f(n) = 2 \cdot \log_2(n) + 2
$$

Where $\log_2(n)$ is the number of iterations of the binary search loop.


We need to find constants $c_1$, $c_2$, and $n_0$ such that:

$$
c_1 \cdot \log_2(n) \leq f(n) \leq c_2 \cdot \log_2(n) \quad \text{for all} \quad n \geq n_0
$$

This will prove that the function $f(n) = 2 \cdot \log_2(n) + 2$ is in $\Theta(\log_2(n))$.

We want to find $c_2$ such that:

$$
2 \cdot \log_2(n) + 2 \leq c_2 \cdot \log_2(n) \quad \text{for large} \ n
$$

For large $n$, the constant $+2$ becomes insignificant compared to the $2 \cdot \log_2(n)$ term. So, we can choose $c_2 = 3$, because:

$$
2 \cdot \log_2(n) + 2 \leq 3 \cdot \log_2(n) \quad \text{for n>4} 
$$

This gives the upper bound.
Now we want to find $c_1$ such that:

$$
2 \cdot \log_2(n) + 2 \geq c_1 \cdot \log_2(n) \quad \text{for large} \ n
$$

Again, for large $n$, the $+2$ term becomes insignificant, and we can choose $c_1 = 2$, because:

$$
2 \cdot \log_2(n) + 2 \geq 2 \cdot \log_2(n) \quad \text{for all} \ n \geq 1
$$

This gives the lower bound.
We can now choose $n_0$ to be any positive integer, say $n_0 = 4$, since the bounds hold for all $n \geq 4$.


We have found constants $c_1 = 2$, $c_2 = 3$, and $n_0 = 4$ such that for all $n \geq n_0$:

$$
2 \cdot \log_2(n) \leq 2 \cdot \log_2(n) + 2 \leq 3 \cdot \log_2(n)
$$

Thus, we have shown that the number of comparisons in binary search is $\Theta(\log_2(n))$ with witnesses. Therefore, the number of comparisons grows logarithmically with the size of the input list, and we have proven the result using the formal definition of $\Theta$-notation with appropriate constants.

## 5. 
Compare these theoretical results with the results you got from your implementation.

list size of 64, following graphs will be offset of 14 to see difference.

![[64.png]]

list size of 78
![[78.png]]

list size of 50
![[50.png]]

Where x is just listsize/2

![[comparison.png]]

## 6.
Assume we have a list of 10,000 elements and need to search for several elements in it. We want to figure out when it pays off to sort the list before searching. Use the $\Theta$ approximations for the following exercises when calculating the number of comparisons made, i.e., assume linear search uses $n$ comparisons and binary search uses $\log_2(n)$ comparisons.

i)
How many comparisons will be used when we search for m elements using linear search?
Linear search is $\Theta(n)$, which is done m times.
The amount of comparisons will be $m\cdot n$ where m is the amount of searches and n is list size which is 10000. 

$10000\cdot m$

 ii) 
We will see that a list of $n$ elements can be sorted with an effort of $\Theta(n \log_2(n))$. How many operations are needed if we sort the list first, then search for $m$ elements using binary search?

In the case of using binary search and an effiecient sorting algorithm, the soring runs in $\Theta(n \log_2(n))$ only once, however binary search is done m times.

$n \log_2(n)+m\cdot \log_2(n)$

replace n with list size.

$10000\cdot \log_2(10000)+m\cdot \log_2(10000)$

$log_2(10000)\approx 13,2877123795$
replace

Total comparisons are, where m is the amount of searches.
$10000\cdot 13,288 + m\cdot 13,288$


iii) At which point, i.e., for which m, do these two approaches have similar complexity? Which one is better when?

This can be done by setting the two comparison formulas equal to eachother and finding when they are equal.

$m \cdot 10000 = 132800 + m \cdot 13,288$

-13.288m both sides

$m \cdot 9986,712 = 132800$

divide with 9986,712

$m  = \frac{132800}{9986,712}$

$m\approx 13.3$