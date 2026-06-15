# Sorting

## Definition

An **ordering relation** < for keys a, b, and c has the following properties:
- Law of Trichotomy: Exactly one of a < b, a = b, b > a is true.
- Law of Transitivity: If a < b, and b < c, then a < c.

A **sort** is a permutation (re-arrangement) of a sequence of elements that puts the keys into non-decreasing order relative to a given ordering relation.

An **inversion** is a pair of elements that are out of order with respect to <.


**Stability**: A sort is said to be stable if order of equivalent items is preserved.
Mergesort, Insertion sort, Counting sort and Radix sort is stable.
Heapsort and Quicksort (LTHS) is not stable.

## Comparison Sorts

**Comparison sorts**:
- Heapsort
- Mergesort
- Quicksort
- Insertion Sort
- Selection Sort
- Bubble Sort
 
### Selection Sort

Selection sorting N items:
- Find the smallest item in the unsorted portion of the array.
- Move it to the end of the sorted portion of the array.
- Selection sort the remaining unsorted items.

**Run Time** $O(N^2)$

### Heap Sort

Heap sort can be viewed as an optimized version of selection sort.
Using **max heap** to select max item.

**In-place heap sort**:
  - Bottom-up heapify input array:
    - Sink nodes in reverse level order.
  - Repeat N times:
    - Delete largest item from the max heap.
    - Swapping root with last item in the heap.
    - Maintain the max heap

**Run Time** $O(N \log N)$
**Extra Memory** $\Theta (N)$ for new heap, $\Theta (1)$ for in-place heap.

### Merge Sort

Mergesort:
- Split items into 2 roughly even pieces.
- Mergesort each half. (Recursively)
- Merge the two sorted halves to form the final result.

**Run Time** $\Theta(N \log n)$
**Extra Memory** $\Theta(N)$

### Insertion Sort

Repeat for i = 0 to N - 1:
- Designate item i as the traveling item.
- Swap item backwards until traveller is in the right place among all previously examined items.

**Run Time** $O (N^2)$
*When the problem's size is small enough, insertion sort is quicker.

### Quick Sort

Quick sorting N items:
- Partition on leftmost item.
- Quicksort left half.
- Quicksort right half.

To partition an array a[] on element x = a[i] (Pivot) is to rearrange a[] so that:
- x moves to position j (may be the same as i)
- All entries to the left of x are <= x.
- All entries to the right of x are >= x.

**Hoare Partitioning**
Create L and G pointers at left and right ends.
- L pointer is a friend to small items, and hates large or equal items.
- G pointer is a friend to large items, and hates small or equal items.
- Walk pointers towards each other, stopping on a hated item.
  - When both pointer have stopped, swap and move pointers by one.
  - When pointers cross, you are done walking.
- Swap pivot with G.

**Run Time** 
- Best case: $\Theta(N \log N)$
- Worst case: $\Theta(N^2)$
- Randomly chosen array case: $\Theta(N\log N)$ expected 

**Extra Memory** $\Theta(\log N)$ (call stack)

### *Quick Select

Quick select finds the k-th smallest item in an unsorted array using partitioning.

It is often used to find the median without fully sorting the array.

**Procedure**
1. Choose a pivot.
2. Partition the array around the pivot.
3. Let p be the final index of the pivot.
4. Compare p with k:
   - If p == k, return A[p].
   - If k < p, search only the left side.
   - If k > p, search only the right side.

**Run Time** $\Theta(N)$ on average

### Theoretical Bounds

Any sort that uses comparisons has runtime $\Omega(N \log N)$.

## Non-comparison Sorts

**Non-comparison sorts**:
- Radix Sort
- Sleepsort
- Gravity Sort
- BOGOsort

### Counting Sort

Counting sort sorts keys by counting how many times each key appears.
- Count the frequency of each key.
- Convert counts into starting positions / cumulative counts.
- Place each item into its correct position in the output array.
- Copy the output array back if needed.

**Run Time** $\Theta(N + R)$

**Extra Memory** $\Theta(N + R)$

### Radix Sort

#### LSD Radix Sort

Least Significant Digit Radix Sort

Digit-by-digit counting sort from the rightmost digit.

**Run Time** $\Theta(WN + WR)$

**Extra Memory** $\Theta(N + R)$

#### MSD Radix Sort

Most Significant Digit Radix Sort

Digit-by-digit counting sort from the leftmost digit.
But, sort each subproblem separately.

**Run Time** $\Theta(N + R)$ (Best), $\Theta(WN + WR)$ (Worst)

**Extra Memory** $\Theta(N + WR)$

*N: Number of keys, R: Size of alphabet, W: Width of longest key.