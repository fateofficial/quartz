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
        int m = l + (r - l) / 2;  
  
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