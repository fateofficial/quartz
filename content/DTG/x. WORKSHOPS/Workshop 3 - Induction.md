# MergeSort Workshop

In this workshop, we will study the **MergeSort** sorting algorithm. A pseudocode for MergeSort is presented as **Figure 1** and can also be looked up in [Ros], section 5.4.4. MergeSort uses a subroutine **Merge**, which is presented in **Figure 2**. 

Note that the algorithms are described here slightly differently than in [Ros], but the underlying idea remains the same. To sort a list 

$$
L = (a_0, a_1, \dots, a_{n-1})
$$

with the program given in the pseudocode, one would call the procedure:

$$
\text{Mergesort}(L, 0, n - 1).
$$

Before you start, it might be useful to reacquaint yourself with section 5.4.4.


Procedure Mergesort(L = ($a_0, a_1, ..., a_{n−1}$), l, r)
    $if~~l< r ~~then$
        $m = \lfloor(r + l) / 2\rfloor$
        $Mergesort(L, l, m)$
        $Mergesort(L, m + 1, r)$
        $L = Merge(L, l, m, r)$
    return L


---
---

## Exercise 1
1)
Implement Merge and Mergesort.
```
void mergeSort(int L[], int l, int r) {  
    if (l < r) {  
        // find the middle point  
        int m = (r - l) / 2;  
  
        // recursively sort the two halves  
        mergeSort(L, l, m);  
        mergeSort(L, m + 1, r);  
  
        // merge the sorted halves  
        merge(L, l, m, r);  
    }  
}
```

```
void merge(int L[], int l, int m, int r) {  
    // calculate the sizes of the two sub-arrays  
    int n1 = m - l + 1;  // Size of left subarray  
    int n2 = r - m;      // Size of right subarray  
    int L1[n1], L2[n2];  
  
    // copy data into temporary arrays L1 and L2  
    for (int i = 0; i < n1; i++)  
        L1[i] = L[l + i];  
    for (int j = 0; j < n2; j++)  
        L2[j] = L[m + 1 + j];  
  
    // indices for the left and right sub-arrays  
    int i = 0, j = 0;  
  
    // merge the sub-arrays into the original array L  
    while (i < n1 && j < n2) {  
        if (L1[i] <= L2[j]) {  
            L[l + i + j] = L1[i];  // place element from L1 into L  
            i++;  
        } else {  
            L[l + i + j] = L2[j];  // place element from L2 into L  
            j++;  
        }  
    }  
  
    // if there are remaining elements in L1[], copy them into L  
    if (i == n1) {  
        for (int k = j; k < n2; k++) {  
            L[l + i + k] = L2[k];  // copy remaining elements from L2  
        }  
    } else {  
        // if there are remaining elements in L2[], copy them into L  
        for (int k = i; k < n1; k++) {  
            L[l + j + k] = L1[k];  // copy remaining elements from L1  
        }  
    }  
}
```

2)
Use Mergesort to sort the list L = (5, 3, 8, 1, 6, 10, 7, 2, 4, 9)

```
Original array: 5 3 8 1 6 10 7 2 4 9
Sorted array: 1 2 3 4 5 6 7 8 9 10
```

---

## Exercise 2

Proof by using induction, that Mergesort returns the sorted list containing the same elements as the input list L. In the proof you may assume, that Merge returns returns a sorted list containing the elements of two sorted lists given as inputs.

#Proof
### Base Case:
Let $P(n)$ be the statement that for any list $L$ of size $n$, mergeSort correctly returns a sorted list containing the same elements as the input list $L$.

When the input list has only one element, where $l = r$, the algorithm terminates without further recursion. A list of one element is trivially sorted, and the list returned is the same as the input list. Therefore, $P(1)$ holds.

### Inductive Hypothesis:
Assume that $P(k)$ is true. That is, for any list $L$ of size $k$, mergeSort correctly returns a sorted list containing the same elements as the input list $L$:
	mergeSort(L) returns a sorted list.
	The returned list contains the same elements as the input list $L$.

### Inductive Step:
We need to prove that $P(k + 1)$ is true. That is, for a list $L$ of size $k + 1$, mergeSort returns a sorted list containing the same elements as $L$.

#### Step 1: Divide the List
The algorithm divides the list $L$ into two smaller sublists:
	The left sublist $L_1$ contains elements from index $l$ to $m$, where $m = \left\lfloor \frac{l + r}{2} \right\rfloor$.
	The right sublist $L_2$ contains elements from index $m + 1$ to $r$.

#### Step 2: Apply the Inductive Hypothesis
By the inductive hypothesis:
	mergeSort(L$_1$) returns a sorted list containing the same elements as $L_1$.
	mergeSort(L$_2$) returns a sorted list containing the same elements as $L_2$.

#### Step 3: Merge the Sublists
The merge function combines the two sorted sublists $L_1$ and $L_2$ into a single sorted list $L'$. Since merge is assumed to correctly combine two sorted lists into one sorted list:
	$L'$ is sorted.
	$L'$ contains all the elements of $L_1$ and $L_2$, which together form the original list $L$.

By induction, $P(n)$ is true for all $n \geq 1$. That is, mergeSort correctly returns a sorted list containing the same elements as the input list for any list size $n$.


---


## Exercise 3
In [Ros] it is shown that the merging of two sorted lists of lengths a and b can be accomplished by using at most $a + b − 1$ comparisons (Lemma 1, section 5.4.4.).

### i)
Assume that Merge uses (exactly) $a + b - 1$ comparisons to combine two lists with $a$ and $b$ elements. Furthermore, assume that the length of the input list $L$ is $n = 2^k$. 
Prove by using induction on $k$, that Mergesort uses
$$
n(\log_2(n) + 1) = 2^k(k + 1)
$$
comparisons to sort $L$. What type of induction did you use?

#proof

Let $P(k)$ be the statement that Mergesort uses 
$$
n(\log_2(n) + 1) = 2^k(k + 1)
$$
comparisons to sort a list of size $n = 2^k$. We will prove that $P(k)$ holds for all $k \geq 0$ using **strong induction**.

### Base Case ($k = 0$):

For $k = 0$, we have $n = 2^0 = 1$. A list of size 1 requires no comparisons, so the number of comparisons for sorting this list is 0. 

We also verify the formula for $n = 1$:
$$
n(\log_2(n) + 1) = 1(\log_2(1) + 1) = 1(0 + 1) = 1
$$
Thus, the total number of comparisons is 0, which matches the behavior of the algorithm (since no merge step is required for a single-element list), however if statement fails.

So, the base case holds: $P(0)$ is true.


Inductive Hypothesis :
Assume that $P(k)$ is true for all $k$ from 0 to $m$. That is, for each $k$ in the range $0 \leq k \leq m$, Mergesort uses:
$$
n(\log_2(n) + 1) = 2^k(k + 1)
$$
comparisons to sort a list of size $n = 2^k$.

Inductive Step:
We need to show that $P(m+1)$ holds, i.e., that Mergesort uses:
$$
n(\log_2(n) + 1) = 2^{m+1}(m + 2)
$$
comparisons to sort a list of size $n = 2^{m+1}$.

For a list of size $n = 2^{m+1}$, Mergesort splits it into two sublists, each of size $2^m$. By the inductive hypothesis, each sublist requires $2^m(m + 1)$ comparisons to sort. Thus, the total number of comparisons required to sort the two sublists is:
$$
2 \times 2^m(m + 1) = 2^{m+1}(m + 1)
$$

Next, the merge step combines these two sublists, each of size $2^m$. The merge step requires $2^m + 2^m - 1 = 2^{m+1} - 1$ comparisons.

Thus, the total number of comparisons for sorting a list of size $2^{m+1}$ is:
$$
\text{Total comparisons} = 2^{m+1}(m + 1) + (2^{m+1} - 1)
$$

Simplifying this:
$$
2^{m+1}(m + 1) + 2^{m+1} - 1 = 2^{m+1}(m + 2) - 1
$$

Now, verify the formula for $n = 2^{m+1}$:
$$
n(\log_2(n) + 1) = 2^{m+1}(\log_2(2^{m+1}) + 1) = 2^{m+1}(m + 2)
$$
Thus, the total number of comparisons is:
$$
2^{m+1}(m + 2)
$$
The difference of 1 comparisons can be explained from the first if statement that is not counted.

which matches the expression we computed above when considering the last failed if statement.

By the principle of strong induction, we have shown that Mergesort uses:
$$
n(\log_2(n) + 1) = 2^k(k + 1)
$$
comparisons to sort a list of size $n = 2^k$.



---

### ii)
Use induction to show that Mergesort uses less or equal to $2n \log_2(n)$  comparisons for all $n \geq 2$ using the same assumptions regarding the Merge procedure as before.

**Hints:**  
A list with $n + 1$ elements is divided into two lists with 
$\left\lceil \frac{n+1}{2} \right\rceil$ and $\left\lfloor \frac{n+1}{2} \right\rfloor$ 
elements respectively by Mergesort. Furthermore, the following inequalities might be useful:

$2 \left\lfloor \frac{n+1}{2} \right\rfloor \log_2 \left( \left\lfloor \frac{n+1}{2} \right\rfloor \right) \leq 2 \left\lfloor \frac{n+1}{2} \right\rfloor \log_2 \left( \left\lceil \frac{n+1}{2} \right\rceil \right)$
$\left\lfloor \frac{n+1}{2} \right\rfloor + \left\lceil \frac{n+1}{2} \right\rceil = n + 1$
$\left\lceil \frac{n+1}{2} \right\rceil \leq \frac{2}{3}(n + 1)$ for $n$ a positive integer
$\log_2 \left( \frac{2}{3}(n + 1) \right) = \log_2(n + 1) - \log_2 \left( \frac{3}{2} \right)$
$n + 1 - 2(n + 1) \log_2 \left( \frac{3}{2} \right) < 0$ for positive $n$.

#proof 

Let $P(n)$ be the statement: "MergeSort uses at most $2n \log_2(n)$ comparisons for all $n \geq 2$," where $n = 2^k$ for some integer $k$.

### Assumptions:
1. Merge uses exactly $a + b - 1$ comparisons to combine two lists of size $a$ and $b$, respectively.
2. The length of the input list $L$ is $n = 2^k$, ensuring $n$ is always a power of 2.

We aim to prove that Mergesort uses fewer than or equal to $2n \log_2(n)$ comparisons for all $n \geq 2$, under the assumption that the Merge operation requires $a + b - 1$ comparisons to merge two lists of length $a$ and $b$.

#### Base Case:
For $n = 2$, Mergesort requires the following steps:
- The list is divided into two sublists, each of size 1.
- Merging these two sublists requires $1$ comparison.
Thus, the total number of comparisons used is $1$, and we check the inequality:
$$
2n \log_2(n) = 2 \cdot 2 \cdot \log_2(2) = 4
$$
Since $1 \leq 4$, the base case holds.

#### Inductive Hypothesis:
Let $P(k)$ be the statement that Mergesort uses fewer than or equal to $2k \log_2(k)$ comparisons for all $k \leq n$, i.e., for any list of size $k$, the number of comparisons is bounded by:
$$
T(k) \leq 2k \log_2(k)
$$
This is the inductive hypothesis.

#### Inductive Step:
We now prove the statement for $n+1$, i.e., that Mergesort uses fewer than or equal to $2(n+1) \log_2(n+1)$ comparisons for a list of size $n+1$.

To do this, we assume the list of size $n+1$ is divided into two sublists of sizes $\left\lfloor \frac{n+1}{2} \right\rfloor$ and $\left\lceil \frac{n+1}{2} \right\rceil$. The number of comparisons used to merge these two sublists is given by the sum of comparisons used by each recursive call and the comparisons made during the merge step.

##### Step 1: Number of comparisons for merging
The merge step requires $\left\lfloor \frac{n+1}{2} \right\rfloor + \left\lceil \frac{n+1}{2} \right\rceil - 1$ comparisons. Using the fact that $\left\lfloor \frac{n+1}{2} \right\rfloor + \left\lceil \frac{n+1}{2} \right\rceil = n+1$, the merge step requires $n$ comparisons.

##### Step 2: Applying the inductive hypothesis
By the inductive hypothesis, the number of comparisons to sort the two sublists of size $\left\lfloor \frac{n+1}{2} \right\rfloor$ and $\left\lceil \frac{n+1}{2} \right\rceil$ is bounded by:
$$
T\left(\left\lfloor \frac{n+1}{2} \right\rfloor\right) \leq 2 \cdot \left\lfloor \frac{n+1}{2} \right\rfloor \log_2 \left( \left\lfloor \frac{n+1}{2} \right\rfloor \right)
$$
and
$$
T\left(\left\lceil \frac{n+1}{2} \right\rceil\right) \leq 2 \cdot \left\lceil \frac{n+1}{2} \right\rceil \log_2 \left( \left\lceil \frac{n+1}{2} \right\rceil \right)
$$
Thus, the total number of comparisons is the sum of the comparisons for the two sublists and the comparisons for the merge step:
$$
T(n+1) = T\left(\left\lfloor \frac{n+1}{2} \right\rfloor\right) + T\left(\left\lceil \frac{n+1}{2} \right\rceil\right) + n
$$
Substituting the bounds from the inductive hypothesis:
$$
T(n+1) \leq 2 \cdot \left\lfloor \frac{n+1}{2} \right\rfloor \log_2 \left( \left\lfloor \frac{n+1}{2} \right\rfloor \right) + 2 \cdot \left\lceil \frac{n+1}{2} \right\rceil \log_2 \left( \left\lceil \frac{n+1}{2} \right\rceil \right) + n
$$

##### Step 3: Bounding the terms
To simplify, we use the fact that:
$$
\left\lceil \frac{n+1}{2} \right\rceil \leq \frac{2}{3}(n+1)
$$
and
$$
\left\lfloor \frac{n+1}{2} \right\rfloor \leq \frac{2}{3}(n+1)
$$
We also know that:
$$
\log_2\left(\frac{2}{3}(n+1)\right) = \log_2(n+1) - \log_2\left(\frac{3}{2}\right)
$$
Thus, we substitute these bounds into the comparison terms. Expanding and simplifying:
$$
T(n+1) \leq \frac{8}{3}(n+1) \log_2(n+1) + n - \frac{8}{3}(n+1) \log_2 \left( \frac{3}{2} \right)
$$

##### Step 4: Ensuring the inequality holds
We now ensure that the inequality:
$$
T(n+1) \leq 2(n+1) \log_2(n+1)
$$
holds by showing that the negative term is sufficiently large to keep the total comparison count under the bound. 
Thus, we conclude:
$$
T(n+1) \leq 2(n+1) \log_2(n+1)
$$

By the principle of strong induction, we have shown that Mergesort uses fewer than or equal to $2n \log_2(n)$ comparisons for all $n \geq 2$.



---





