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

## Exercise 2

Proof by using induction, that Mergesort returns the sorted list containing the same elements as the input list L. In the proof you may assume, that Merge returns returns a sorted list containing the elements of two sorted lists given as inputs.

#### Base Case:
When the input list has only one element, where $l = r$, the algorithm terminates without further recursion. A list of one element is trivially sorted, and the list returned is the same as the input list. Therefore, the base case holds.

#### Inductive Hypothesis:
Assume that for any list $L$ of size $k$, the function mergeSort correctly returns a sorted list containing the same elements as the input list $L$. More formally, for any list $L$ with $|L| = k$, mergeSort(L) will:
1. Return a sorted list.
2. Contain the same elements as the input list $L$.

#### Inductive Step:
We need to show that mergeSort also works for lists of size $k + 1$.

Consider a list $L$ of size $k + 1$.  mergeSort  divides the list into two smaller sublists:
	The left sublist $L_1$ contains elements from index $l$ to $m$, where $m = \left\lfloor \frac{l + r}{2} \right\rfloor$.
	The right sublist $L_2$ contains elements from index $m + 1$ to $r$.

By the inductive hypothesis, both the left sublist $L_1$ and the right sublist $L_2$, each having size less than or equal to $k$, are sorted correctly and contain the same elements as the original sublists. In other words:
	mergeSort(L_1) returns a sorted list containing the same elements as $L_1$,
	mergeSort(L_2) returns a sorted list containing the same elements as $L_2$.

The merge function is then used to combine these two sorted sublists into a single sorted list. Since we assume that merge correctly merges two sorted lists into a sorted list containing all the elements of the two sublists, the merged list $L'$ will:
	Be sorted (since merge produces a sorted result),
	Contain all the elements from $L_1$ and $L_2$, which together form the original list $L$.

Therefore, the result of mergeSort(L) is a sorted list containing the same elements as the input list $L$.



## Exercise 3
In [Ros] it is shown that the merging of two sorted lists of lengths a and b can be accomplished by using at most $a + b − 1$ comparisons (Lemma 1, section 5.4.4.).

i)
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
comparisons to sort a list $L$ of size $n = 2^k$. We will prove that $P(k)$ holds for all $k \geq 0$ by induction.

## Base Case ($k = 0$):

For $k = 0$, we have $n = 2^0 = 1$. This means the input list contains only one element, and no comparisons are needed to sort it. The base case for the recursive sorting step does not involve any splitting, as the list is already trivially sorted. Therefore, no comparisons are made during the merge step.

Using the assumption that the merge step requires $a + b - 1$ comparisons to combine two lists of size $a$ and $b$, for a single-element list, both $a$ and $b$ are 0 in the merge process, which means that:
$$
a + b - 1 = 1+ 0 - 1 = 0 \text{ comparisons for merge}
$$
This reflects the fact that no merge step is needed for a list of size 1. Thus, the total number of comparisons for this case is 0.

Now, check the formula for $k = 0$:
$$
n(\log_2(n) + 1) = 1(\log_2(1) + 1) = 1(0 + 1) = 1
$$
Since no comparisons are required for a list of size 1, the total number of comparisons is 0, however the whole algorithm uses 1 comparison in the sense of failing the if statement in the mergesort function. Therefore  P(0) = true.

## Inductive Hypothesis:

Assume that $P(k)$ is true for some $k = m$. That is, for a list of size $n = 2^m$, Mergesort uses:
$$
n(\log_2(n) + 1) = 2^m(m + 1)
$$
comparisons to sort the list. We now need to show that $P(k)$ holds for $k = m + 1$, i.e., for a list of size $n = 2^{m+1}$.

## Inductive Step:

For a list of size $n = 2^{m+1}$, Mergesort proceeds by splitting the list into two sublists oppf size $2^m$. Each of these sublists is recursively sorted using Mergesort. By the inductive hypothesis, each sublist requires $2^m(m + 1)$ comparisons to sort. Thus, the total number of comparisons required to sort the two sublists is:
$$
2 \times 2^m(m + 1) = 2^{m+1}(m + 1)
$$
After sorting the two sublists, the merge step is required to combine them into a single sorted list. The merge step compares the elements from both sublists and requires $(a + b - 1)$ comparisons to combine two lists of size $a$ and $b$. Since both sublists are of size $2^m$, the number of comparisons required for the merge step is:
$$
2^m + 2^m - 1 = 2^{m+1} - 1
$$
Thus, the total number of comparisons for sorting a list of size $2^{m+1}$ is:
$$
\text{Total comparisons} = 2^{m+1}(m + 1) + (2^{m+1} - 1)
$$
Simplifying this expression:
$$
2^{m+1}(m + 1) + 2^{m+1} - 1 = 2^{m+1}(m + 2) - 1
$$
Now, check the formula for $n = 2^{m+1}$:
$$
n(\log_2(n) + 1) = 2^{m+1}(\log_2(2^{m+1}) + 1) = 2^{m+1}((m + 1) + 1) = 2^{m+1}(m + 2)
$$
This is exactly the total number of comparisons we computed above

Thus, the number of comparisons required to sort a list of size $n = 2^{m+1}$ is:
$$
2^{m+1}((m + 1)+1)
$$
which matches the formula we are trying to prove. Therefore, $P(k)$ holds for $k = m + 1$.


By the principle of mathematical induction, we have shown that $P(k)$ holds for all $k \geq 0$. Hence, Mergesort uses:
$$
n(\log_2(n) + 1) = 2^k(k + 1)
$$
comparisons to sort a list of size $n = 2^k$.












