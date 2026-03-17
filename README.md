# Sorting-and-searching-


- [SORTING](#SORTING)
- [SEARCHING](#SEARCHING)
- [BINARY SEARCHING](#BINARY-SEARCHING)


# SORTING 

### index
##### sorting
- [bubble sort](#bubble-sort)
- [insertion sort](#insertion-sort)
- [selection sort](#selection-sort)
- [merge sort](#merge-sort)
- [quick sort](#quick-sort)
- [heap sort](#heap-sort)
- [comparison](#comparison)
- [sorting visualizer](https://visualgo.net/en/sorting)
  

#### bubble sort 
#### algorithm
* iterate , compare two adjacent elem and sort 
```
 for(i  = 0 to n-1 , i++)   //if n = 5 , n-1 = 4 so loop run from 0 to 4
    for(j = 0 to n-1-i j++)   //if the previouuse index in sorted we minus i to minimize the iteration 
        compare if(a[j]>a[j+1])  // the element is larger than the next next element or not 
                temp=a[j];       |
                a[j]=a[j+1];     | - -  // swaping j and j+1
                a[j+1]=temp;     |
```

#### code 
```c
#include <stdio.h>
#include <conio.h>

int main()
{
    int i,j,n,temp;
    printf("enter size of array");
    scanf("%d",&n);
    int a[n];
    printf("enter elements of array");
    for(i=0;i<n;i++){
        scanf("%d",&a[i]);
    }
    for(i=0;i<n-1;i++){
        for(j=0;j<n-1-i;j++){
            if(a[j]>a[j+1]){
                temp=a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
            }
        }
    }
    for(i=0;i<n;i++){
        printf("%d",a[i]);
    }
    
    return 0;
}
```
#### insertion sort
#### algorithm
* devide , comre with previous , find correct position , insert
```
devide the given list into two part sorted and unsorted
initially the first element is considered sorted list  [ sorted  |     unsorted    ]

for(i  = 1 to n , i++)   //if n = 5 loop run from 1 to 4, 0 is considered sorted
    temp=a[i];   // take the element in temprory variable 
    j=i-1;    // as we wii compare the element with elem in sorted list 
    while(j>=0 && a[j]>temp)   // while the sorted list has no elem left and check if the elem is greater or not to find the right place
        a[j+1]=a[j];   // shift element to the right 
        j--;   // decrement j
        }
        a[j+1]=temp;  // store elem at right place 

```

#### code 
```c
#include <stdio.h>
#include <conio.h>

int main()
{
    int i,j,n,temp;
    printf("enter size of array");
    scanf("%d",&n);
    int a[n];
    printf("enter elements of array");
    for(i=0;i<n;i++){
        scanf("%d",&a[i]);
    }
    for(i=1;i<n;i++){
        temp=a[i];
        j=i-1;
        while(j>=0 && a[j]>temp){
            a[j+1]=a[j];
            j--;
        }
        a[j+1]=temp;
                  
    }
    for(i=0;i<n;i++){
        printf("%d",a[i]);
    }
    
    return 0;
}
```

#### selection sort
#### algorithm
find min elem , swap it with the (0 to n) index 
```
 for(i  = 0 to n-1 , i++)   // if n = 5 , n-1 = 4 so loop run from 0 to 4
     min=i;  
     for(j = i+1 to n , j++)   // if n = 5 , i+1 = 1 
         if(a[j]<a[min])     // if j < min
         min=j;    // take j as min
         if(min!=i){
            temp=a[i];       |
            a[i]=a[min];     | --- // swap min with i ( if min != i)
            a[min]=temp;     | 
        }
```

#### code 
```c
#include <stdio.h>
#include <conio.h>

int main()
{
    int i,j,n,temp;
    printf("enter size of array");
    scanf("%d",&n);
    int a[n];
    printf("enter elements of array");
    for(i=0;i<n;i++){
        scanf("%d",&a[i]);
    }
    for(i=0;i<n-1;i++){
        int min=i;
        for(j=i+1;j<n;j++){
            if(a[j]<a[min]){
                min=j;
            }
        }
        if(min!=i){
            temp=a[i];
            a[i]=a[min];
            a[min]=temp;
        }
            
        
    }
    for(i=0;i<n;i++){
        printf("%d",a[i]);
    }
    
    return 0;
}
```

##### merge sort
#### algorithm 
devide from mid upto one elem , merge 
```
void mergeSort(int A[], int lb, int ub) 
    if (lb < ub) 
        int mid = (lb + ub) / 2;

        mergeSort(A, lb, mid);  // devide from start to half
        mergeSort(A, mid + 1, ub);  // devide from half to last 
        merge(A, lb, mid, ub);   // merging
```
#### code     
```c
#include <stdio.h>

void merge(int A[], int lb, int mid, int ub) {
    int i = lb;
    int j = mid + 1;
    int k = lb;

    int B[1000]; // temporary array (you can also malloc dynamically)

    // merging of element in the temprory array
    while (i <= mid && j <= ub) {
        if (A[i] <= A[j]) {
            B[k] = A[i];
            i++;
        } else {
            B[k] = A[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements from left part
    while (i <= mid) {
        B[k] = A[i];
        i++;
        k++;
    }

    // Copy remaining elements from right part
    while (j <= ub) {
        B[k] = A[j];
        j++;
        k++;
    }

    // Copy back to original array
    for (i = lb; i <= ub; i++) {
        A[i] = B[i];
    }
}

void mergeSort(int A[], int lb, int ub) {
    if (lb < ub) {
        int mid = (lb + ub) / 2;

        mergeSort(A, lb, mid);
        mergeSort(A, mid + 1, ub);
        merge(A, lb, mid, ub);
    }
}

int main() {
    int A[50], n;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements:\n", n);
    for (int i = 0; i < n; i++)
        scanf("%d", &A[i]);

    mergeSort(A, 0, n - 1);

    printf("Sorted array:\n");
    for (int i = 0; i < n; i++)
        printf("%d ", A[i]);

    return 0;
}
```

##### quick sort
```cpp
#include <stdio.h>

int partition(int A[], int lb, int ub)
{
    int pivot = A[lb];
    int start = lb;
    int end = ub;
    int temp;

    while (start < end)
    {
        while (A[start] <= pivot)
            start++;

        while (A[end] > pivot)
            end--;

        if (start < end)
        {
            temp = A[start];
            A[start] = A[end];
            A[end] = temp;
        }
    }

    temp = A[lb];
    A[lb] = A[end];
    A[end] = temp;

    return end;
}

void quickSort(int A[], int lb, int ub)
{
    if (lb < ub)
    {
        int loc = partition(A, lb, ub);
        quickSort(A, lb, loc - 1);
        quickSort(A, loc + 1, ub);
    }
}

int main()
{
    int A[50], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for (i = 0; i < n; i++)
        scanf("%d", &A[i]);

    quickSort(A, 0, n - 1);

    printf("Sorted array:\n");
    for (i = 0; i < n; i++)
        printf("%d ", A[i]);

    return 0;
}
```

#### heap sort

### Heap 
* **Heap** → Complete Binary Tree
* Stored using **array**
* Indexing (1-based):

  * Parent = `i/2`floar
  * Left child = `2i`
  * Right child = `2i+1`

### Max Heap

**Property:**
`Parent ≥ Children`
👉 Maximum element is at **root**

#### Example

```
        70
      /    \
    60      40
   /  \    /  \
 50  35  39  16
```

### Min Heap

**Property:**
`Parent ≤ Children`
👉 Minimum element is at **root**

#### Example

```
        10
      /    \
    20      30
   /  \    /  \
 40  50  60  70
```

### MAX HEAP OPERATIONS

#### Max Heap Insertion
parent node = [i/2]floar
TC = O(log n) -> height of heap
```c
void insertMaxHeap(int A[], int *n, int value)
{
    (*n)++;
    int i = *n;
    A[i] = value;

    while (i > 1 && A[i/2] < A[i])
    {
        int temp = A[i];
        A[i] = A[i/2];
        A[i/2] = temp;
        i = i/2;
    }
}
```

#### Max Heap Deletion (Delete Root)

```c
void deleteMaxHeap(int A[], int *n)
{
    if (*n == 0) return;

    A[1] = A[*n];
    (*n)--;

    int i = 1;
    while (2*i <= *n)
    {
        int largest = i;
        int left = 2*i;
        int right = 2*i + 1;

        if (left <= *n && A[left] > A[largest])
            largest = left;

        if (right <= *n && A[right] > A[largest])
            largest = right;

        if (largest != i)
        {
            int temp = A[i];
            A[i] = A[largest];
            A[largest] = temp;
            i = largest;
        }
        else
            break;
    }
}
```

### MIN HEAP OPERATIONS 

#### Min Heap Insertion

```c
void insertMinHeap(int A[], int *n, int value)
{
    (*n)++;
    int i = *n;
    A[i] = value;

    while (i > 1 && A[i/2] > A[i])
    {
        int temp = A[i];
        A[i] = A[i/2];
        A[i/2] = temp;
        i = i/2;
    }
}
```

#### Min Heap Deletion (Delete Root)

```c
void deleteMinHeap(int A[], int *n)
{
    if (*n == 0) return;

    A[1] = A[*n];
    (*n)--;

    int i = 1;
    while (2*i <= *n)
    {
        int smallest = i;
        int left = 2*i;
        int right = 2*i + 1;

        if (left <= *n && A[left] < A[smallest])
            smallest = left;

        if (right <= *n && A[right] < A[smallest])
            smallest = right;

        if (smallest != i)
        {
            int temp = A[i];
            A[i] = A[smallest];
            A[smallest] = temp;
            i = smallest;
        }
        else
            break;
    }
}
```

### Time Complexity 

| Operation | Time     |
| --------- | -------- |
| Insertion | O(log n) |
| Deletion  | O(log n) |
| Heapify   | O(log n) |

### heapify 
BUILD-MAX-HEAP(A, n)     → O(n)
for i = n down to 2 //largest non leaf node (n/2)  if index start from 0 (n/2 - 1)
    exchange A[1] ↔ A[i]
    heap-size = heap-size - 1
    MAX-HEAPIFY(A, 1)

#### max heapify
```cpp
#include <bits/stdc++.h>
using namespace std;

void maxHeapify(vector<int> &A, int n, int i) {
    int largest = i;
    int left = 2*i + 1;      // left child
    int right = 2*i + 2;     // right child

    // If left child is larger than root
    if(left < n && A[left] > A[largest])
        largest = left;

    // If right child is larger than largest so far
    if(right < n && A[right] > A[largest])
        largest = right;

    // If largest is not root
    if(largest != i) {
        swap(A[i], A[largest]);
        maxHeapify(A, n, largest);  // recursively heapify
    }
}

int main() {
    vector<int> A = {4, 10, 3, 5, 1};
    int n = A.size();

    // Build Max Heap
    for(int i = n/2 - 1; i >= 0; i--) {
        maxHeapify(A, n, i);
    }

    cout << "Max Heap: ";
    for(int x : A)
        cout << x << " ";

    return 0;
}
```



---













# SEARCHING 

### 🔍 Linear Search 

```c
int main()
{
    int a[50], n, key, i;

    scanf("%d", &n);
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    scanf("%d", &key);

    for (i = 0; i < n; i++)
        if (a[i] == key)
        {
            printf("Found at %d", i);
            return 0;
        }

    printf("Not found");
    return 0;
}
```

---

### 🔍 Binary Search — **main only** (sorted array)

```c
int main()
{
    int a[50], n, key, low = 0, high, mid, i;

    scanf("%d", &n);
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);

    scanf("%d", &key);
    high = n - 1;

    while (low <= high)
    {
        mid = (low + high) / 2;

        if (a[mid] == key)
        {
            printf("Found at %d", mid);
            return 0;
        }
        else if (a[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }

    printf("Not found");
    return 0;
}
```

















## comparison 

---

## 🔍 Searching Algorithms

* **Linear Search** → Best: **O(1)** | Average: **O(n)** | Worst: **O(n)**
* **Binary Search** → Best: **O(1)** | Average: **O(log n)** | Worst: **O(log n)**

---

## 🔃 Sorting Algorithms

* **Bubble Sort** → Best: **O(n)** | Average: **O(n²)** | Worst: **O(n²)**
* **Selection Sort** → Best/Average/Worst: **O(n²)**
* **Insertion Sort** → Best: **O(n)** | Average: **O(n²)** | Worst: **O(n²)**
* **Merge Sort** → Best/Average/Worst: **O(n log n)**
* **Quick Sort** → Best/Average: **O(n log n)** | Worst: **O(n²)**
* **Heap Sort** → Best/Average/Worst: **O(n log n)**
* **Counting Sort** → Best/Average/Worst: **O(n + k)**
* **Radix Sort** → Best/Average/Worst: **O(d(n + k))**
* **Bucket Sort** → Best/Average: **O(n + k)** | Worst: **O(n²)**

---

---
```cpp
+---------------------------+-----------------------------+------------------------------+
|        BUBBLE SORT        |        INSERTION SORT       |        SELECTION SORT        |
+---------------------------+-----------------------------+------------------------------+
| for(i=0;i<n-1;i++){       | for(i=1;i<n;i++){           | for(i=0;i<n-1;i++){          |
|   for(j=0;j<n-1-i;j++){   |   temp=a[i];                |   int min=i;                 |
|     if(a[j]>a[j+1]){      |   j=i-1;                    |   for(j=i+1;j<n;j++){        |
|       temp=a[j];          |   while(j>=0 &&             |     if(a[j]<a[min]){         |
|       a[j]=a[j+1];        |        a[j]>temp){          |       min=j;                 |
|       a[j+1]=temp;        |     a[j+1]=a[j];            |     }                        |
|     }                     |     j--;                    |   }                          |
|   }                       |   }                         |   if(min!=i){                |
| }                         |   a[j+1]=temp;              |     temp=a[i];               |
|                           | }                           |     a[i]=a[min];             |
|                           |                             |     a[min]=temp;             |
|                           |                             |   }                          |
|                           |                             | }                            |
+---------------------------+-----------------------------+------------------------------+

```
---













# BINARY SEARCHING 

**Binary Search[1D,2D,Array,Search Space]**

#### BS on 1D Arrays
- [basic](#basic)
- [implement lower bound](#Lower-Bound)
- [implement upper bound](#Upper-Bound)
- [search insert position](#Search-Insert-Position)
- [floor/ceil in sorted array](#FloorCeil-in-Sorted-Array)
- [find the first or last occurrence of a given number in a sorted array](#find-the-first-or-last-occurrence-of-a-given-number-in-a-sorted-array)
- [count occurrences of a number in a sorted array with duplicates](#count-occurrences-of-a-number-in-a-sorted-array-with-duplicates)
- [count occurrences of a number in a sorted array with duplicates](#count-occurrences-of-a-number-in-a-sorted-array-with-duplicates)
- [search in rotated sorted array i](#search-in-rotated-sorted-array-i)
- [search in rotated sorted array ii](#search-in-rotated-sorted-array-ii)
- [find minimum in rotated sorted array](#find-minimum-in-rotated-sorted-array)
- [find out how many times has an array been rotated](#find-out-how-many-times-has-an-array-been-rotated)
- [single element in a sorted array](#single-element-in-a-sorted-array)
- [find peak element](#find-peak-element)

#### BS on Answers

- [find square root of a number in log n](#find-square-root-of-a-number-in-log-n)
- [find the nth root of a number using binary search](#find-the-nth-root-of-a-number-using-binary-search)
- [koko eating bananas](#koko-eating-bananas)
- [minimum days to make m bouquets](#minimum-days-to-make-m-bouquets)
- [find the smallest divisor](#find-the-smallest-divisor)
- [capacity to ship packages within d days](#capacity-to-ship-packages-within-d-days)
- [kth missing positive number](#kth-missing-positive-number)
- [aggressive cows](#aggressive-cows)
- [book allocation problem](#book-allocation-problem)
- [split array - largest sum](#split-array---largest-sum)
- [painter's partition](#painters-partition)
- [minimize max distance to gas station](#minimize-max-distance-to-gas-station)
- [median of 2 sorted arrays](#median-of-2-sorted-arrays)
- [kth element of 2 sorted arrays](#kth-element-of-2-sorted-arrays)

#### BS on 2D Arrays

- [row with maximum numbers of ones](#row-with-maximum-numbers-of-ones)
- [search in 2D matrix I](#search-in-2D-matrix-I)
- [search in 2D matrix II](#search-in-2D-matrix-II)
- [find peak elements II](#find-peak-elements-II)
- [median in a row wise sorted matrix](#median-in-a-row-wise-sorted-matrix)



---
## basic 
### Real Life Example

Example: Searching a word in a dictionary

* Open middle page
* If your word comes before → go left
* If after → go right
* Repeat

You eliminate **half** every step. <br>
That’s why time complexity is **log n**.

### Coding Problem Example

#### Problem:

Find index of `key` in sorted array.

```
Input:
arr = {1,3,5,7,9,11}
key = 7

Output:
3
```

### Iterative Code (Most Asked in Interviews)

```cpp
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] == key)
            return mid;

        else if(arr[mid] < key)
            low = mid + 1;

        else
            high = mid - 1;
    }

    return -1;
}
```


### Recursive Code

```cpp
int binarySearch(int arr[], int low, int high, int key) {

    if(low > high)
        return -1;

    int mid = low + (high - low) / 2;

    if(arr[mid] == key)
        return mid;

    else if(arr[mid] < key)
        return binarySearch(arr, mid + 1, high, key);

    else
        return binarySearch(arr, low, mid - 1, key);
}
```

Call like:

```cpp
binarySearch(arr, 0, n-1, key);
```

### Time Complexity

* Iterative → O(log n)
* Recursive → O(log n) 

#### Space Complexity

* Iterative → O(1)
* Recursive → O(log n) (stack space)

### Overflow Case

Wrong way:

```cpp
int mid = (low + high) / 2;
```

If `low` and `high` are very large → integer overflow.

Correct way:

```cpp
int mid = low + (high - low) / 2;
```

This prevents overflow.


---










## Lower Bound 

Definition : **Lower Bound = First index where element ≥ target**
<br>
It gives:

* First occurrence of target
* Or position where target should be inserted
<br>
Array must be sorted
<br>
<br>
Example :

```cpp
arr = {1, 2, 3, 3, 5, 8, 8, 10, 11}
target = 8

Output → 5 (first 8)

```

### Code 

```cpp
int lowerBound(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    int ans = n;  // default if not found

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] >= target) {
            ans = mid;
            high = mid - 1;  // search left
        }
        else {
            low = mid + 1;   // search right
        }
    }

    return ans;
}
```

---


## Upper Bound

Definition : **Upper Bound = First index where element > target**
<br>
Array must be **sorted**
<br>
<br>
Example : 
```cpp
arr = {1, 2, 3, 3, 5, 8, 8, 10, 11}
target = 8

Output → 7 (first element > 8 → 10)

```

### Code 

```cpp
int upperBound(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    int ans = n;  // default if not found

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] > target) {
            ans = mid;
            high = mid - 1;  // search left
        }
        else {
            low = mid + 1;   // search right
        }
    }

    return ans;
}
```

### STL Version

```cpp
#include <algorithm>

int idx = upper_bound(arr, arr + n, target) - arr;
```

---


## Search Insert Position

```cpp
#include <bits/stdc++.h>
using namespace std;

int searchInsert(vector<int>& arr, int x) {

    int n = arr.size();
    int low = 0, high = n - 1;
    int ans = n;   // default position if x is greater than all elements

    while(low <= high) {

        int mid = low + (high - low) / 2;  // avoid overflow

        // maybe an answer
        if(arr[mid] >= x) {
            ans = mid;
            high = mid - 1;   // look on left for smaller index
        }
        else {
            low = mid + 1;    // look on right
        }
    }

    return ans;
}

int main() {
    vector<int> arr = {1, 3, 5, 6};

    cout << searchInsert(arr, 5) << endl; // 2
    cout << searchInsert(arr, 2) << endl; // 1
    cout << searchInsert(arr, 7) << endl; // 4
    cout << searchInsert(arr, 0) << endl; // 0

    return 0;
}
```

## FloorCeil in Sorted Array

```cpp
int findFloor(int arr[], int n, int x) {
    int low = 0, high = n - 1;
    int ans = -1;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] <= x) {
            ans = arr[mid];
            low = mid + 1;   // search right
        }
        else {
            high = mid - 1;  // search left
        }
    }

    return ans;
}
```


## find the first or last occurrence of a given number in a sorted array

#### Approach

* **First occurrence → lowerBound**
* **Last occurrence → upperBound - 1**

* BETTER APPROACH
```cpp
#include <iostream>
#include <vector>
using namespace std;

int lowerBound(vector<int>& arr, int n, int x) {
    int low = 0, high = n - 1;
    int ans = n;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] >= x) {
            ans = mid;
            high = mid - 1;
        }
        else {
            low = mid + 1;
        }
    }
    return ans;
}

int upperBound(vector<int>& arr, int n, int x) {
    int low = 0, high = n - 1;
    int ans = n;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] > x) {
            ans = mid;
            high = mid - 1;
        }
        else {
            low = mid + 1;
        }
    }
    return ans;
}

pair<int, int> firstAndLastPosition(vector<int>& arr, int n, int k) {

    int lb = lowerBound(arr, n, k);

    if(lb == n || arr[lb] != k)
        return {-1, -1};

    int ub = upperBound(arr, n, k);

    return {lb, ub - 1};
}

int main() {
    vector<int> arr = {1,2,2,2,3,4,5};
    int n = arr.size();
    int k = 2;

    pair<int,int> ans = firstAndLastPosition(arr, n, k);

    cout << "First: " << ans.first << endl;
    cout << "Last: " << ans.second << endl;
}
```

```
First: 1
Last: 3
```

* OPTIMAL APPROACH

```cpp

// Find First Occurrence

int firstOccurrence(int arr[], int n, int x) {
    int low = 0, high = n - 1;
    int first = -1;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] == x) {
            first = mid;
            high = mid - 1;   // move left
        }
        else if(arr[mid] < x) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return first;
}


// Find Last Occurrence

int lastOccurrence(int arr[], int n, int x) {
    int low = 0, high = n - 1;
    int last = -1;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] == x) {
            last = mid;
            low = mid + 1;   // move right
        }
        else if(arr[mid] < x) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return last;
}


// Combined Function

pair<int,int> firstAndLast(int arr[], int n, int x) {
    int first = firstOccurrence(arr, n, x);
    int last = lastOccurrence(arr, n, x);
    return {first, last};
}
```


| Feature             | First/Last Code | LB + UB Code       |
| ------------------- | --------------- | ------------------ |
| Time Complexity     | O(log n)        | O(log n)           |
| Readability         | Easy            | Clean & structured |
| Reusable            | ❌ Not much      | ✅ Highly reusable  |
| Interview Preferred | ✅               | ⭐⭐⭐ More preferred |




## search in rotated sorted array i
```cpp
int search(vector<int>& arr, int n, int k) {
    int low = 0, high = n - 1;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(arr[mid] == k)
            return mid;

        // Left half is sorted
        if(arr[low] <= arr[mid]) {

            if(arr[low] <= k && k <= arr[mid])
                high = mid - 1;
            else
                low = mid + 1;
        }

        // Right half is sorted
        else {

            if(arr[mid] <= k && k <= arr[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }

    return -1;
}
```

## search in rotated sorted array ii

* for duplicates
* when the left right checking wont work -> [3,1,2,3,3,3,3]
```cpp
bool searchInARotatedSortedArrayII(vector<int>& arr, int k) {
    int n = arr.size();
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == k)
            return true;

        // If duplicates at edges
        if (arr[low] == arr[mid] && arr[mid] == arr[high]) {
            low++;
            high--;
            continue;
        }

        // Left half sorted
        if (arr[low] <= arr[mid]) {
            if (arr[low] <= k && k <= arr[mid])
                high = mid - 1;
            else
                low = mid + 1;
        }
        // Right half sorted
        else {
            if (arr[mid] <= k && k <= arr[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }

    return false;
}
```


## find minimum in rotated sorted array
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMin(vector<int>& arr) {
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        // If left part is sorted
        if (arr[low] <= arr[mid]) {
            ans = min(ans, arr[low]);
            low = mid + 1;
        }
        else {  // Right part sorted
            ans = min(ans, arr[mid]);
            high = mid - 1;
        }
    }
    return ans;
}
```

```cpp
// optimal 
int findMin(vector<int>& arr)
{
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;

    while(low <= high) {
        int mid = (low + high) / 2;

        // If whole search space is sorted
        if(arr[low] <= arr[high]) {
            ans = min(ans, arr[low]);
            break;
        }

        // Left half sorted
        if(arr[low] <= arr[mid]) {
            ans = min(ans, arr[low]);
            low = mid + 1;
        }
        // Right half sorted
        else {
            ans = min(ans, arr[mid]);
            high = mid - 1;
        }
    }
    return ans;
}
```


## find out how many times has an array been rotated
```cpp
int findMinIndex(vector<int>& arr) {
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;
    int index = -1;

    while (low <= high) {
        int mid = (low + high) / 2;

        // If whole search space is sorted
        if (arr[low] <= arr[high]) {
            if (arr[low] < ans) {
                ans = arr[low];
                index = low;
            }
            break;
        }

        // If left half is sorted
        if (arr[low] <= arr[mid]) {
            if (arr[low] < ans) {
                ans = arr[low];
                index = low;
            }
            low = mid + 1;
        }
        else {  // Right half is sorted
            if (arr[mid] < ans) {
                ans = arr[mid];
                index = mid;
            }
            high = mid - 1;
        }
    }

    return index;
}
```


## single element in a sorted array
```cpp
int singleNonDuplicate(vector<int>& arr) {
    int n = arr.size();

    if(n == 1) return arr[0];

    for(int i = 0; i < n; i++) {

        if(i == 0) {
            if(arr[i] != arr[i+1]) return arr[i];
        }
        else if(i == n-1) {
            if(arr[i] != arr[i-1]) return arr[i];
        }
        else {
            if(arr[i] != arr[i-1] && arr[i] != arr[i+1])
                return arr[i];
        }
    }
    return -1;
}
```

* with binary search
```cpp
int singleNonDuplicate(vector<int>& arr)
{
    int n = arr.size();

    if(n == 1) return arr[0];

    if(arr[0] != arr[1]) return arr[0];
    if(arr[n-1] != arr[n-2]) return arr[n-1];

    int low = 1, high = n - 2;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        // If mid is the single element
        if(arr[mid] != arr[mid+1] && arr[mid] != arr[mid-1])
            return arr[mid];

        // We are in left half (valid pairing side)
        if((mid % 2 == 1 && arr[mid] == arr[mid-1]) ||
           (mid % 2 == 0 && arr[mid] == arr[mid+1])) {
            low = mid + 1;
        }
        else {   // We are in right half
            high = mid - 1;
        }
    }

    return -1; // Safety return
}
```


## find peak element
```cpp
int findPeakElement(vector<int> &arr)
{
    int n = arr.size();

    if(n == 1) return 0;

    if(arr[0] > arr[1]) return 0;
    if(arr[n-1] > arr[n-2]) return n-1;

    int low = 1, high = n - 2;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        // If mid is peak
        if(arr[mid] > arr[mid-1] && arr[mid] > arr[mid+1]) {
            return mid;
        }
        // If increasing, move right
        else if(arr[mid] > arr[mid-1]) {
            low = mid + 1;
        }
        // Else move left
        else {
            high = mid - 1;
        }
    }

    return -1;  // safety return
}
```


### BS on Answers

### find square root of a number in log n
```cpp
int floorSqrt(int n)
{
    int low = 1, high = n;
    int ans = 0;

    while(low <= high) {
        long long mid = low + (high - low) / 2;
        long long val = mid * mid;

        if(val <= n) {
            ans = mid;        // store possible answer
            low = mid + 1;    // try bigger value
        }
        else {
            high = mid - 1;   // go smaller
        }
    }

    return ans;
}
```






### find the nth root of a number using binary search
```cpp
// return 1 if == m
// return 0 if < m
// return 2 if > m
int func(int mid, int n, int m) {
    long long ans = 1;

    for(int i = 1; i <= n; i++) {
        ans = ans * mid;

        if(ans > m) return 2;   // exceeded
    }

    if(ans == m) return 1;     // exact match
    return 0;                  // less than m
}

int NthRoot(int n, int m) {
    int low = 1, high = m;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        int midN = func(mid, n, m);

        if(midN == 1) {
            return mid;
        }
        else if(midN == 0) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return -1;   // if no integer nth root exists
}
```

### koko eating bananas
```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <climits>
using namespace std;

// Find maximum pile
int findMax(vector<int> &v) {
    int maxi = INT_MIN;
    for(int i = 0; i < v.size(); i++) {
        maxi = max(maxi, v[i]);
    }
    return maxi;
}

// Calculate total hours needed at given speed
int calculateTotalHours(vector<int> &v, int hourly) {
    int totalH = 0;
    for(int i = 0; i < v.size(); i++) {
        totalH += ceil((double)v[i] / hourly);
    }
    return totalH;
}

// Main function
int minimumRateToEatBananas(vector<int> v, int h) {
    int low = 1, high = findMax(v);

    while(low <= high) {
        int mid = low + (high - low) / 2;

        int totalH = calculateTotalHours(v, mid);

        if(totalH <= h) {
            high = mid - 1;   // try smaller speed
        }
        else {
            low = mid + 1;    // increase speed
        }
    }

    return low;   // minimum valid speed
}
```



### minimum days to make m bouquets
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

// Check if possible to make m bouquets
bool possible(vector<int> &arr, int day, int m, int k) {
    int cnt = 0;
    int noOfB = 0;

    for(int i = 0; i < arr.size(); i++) {

        if(arr[i] <= day) {
            cnt++;
        }
        else {
            noOfB += (cnt / k);
            cnt = 0;
        }
    }

    // remaining flowers
    noOfB += (cnt / k);

    return noOfB >= m;
}

int roseGarden(vector<int> arr, int m, int k) {

    long long totalFlowersNeeded = 1LL * m * k;
    if(totalFlowersNeeded > arr.size()) return -1;

    int mini = INT_MAX, maxi = INT_MIN;

    for(int i = 0; i < arr.size(); i++) {
        mini = min(mini, arr[i]);
        maxi = max(maxi, arr[i]);
    }

    int low = mini, high = maxi;

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(possible(arr, mid, m, k)) {
            high = mid - 1;   // try smaller day
        }
        else {
            low = mid + 1;
        }
    }

    return low;
}
```



### find the smallest divisor
```cpp
#include <bits/stdc++.h>
using namespace std;

// Calculate sum after dividing with ceil
int sumByD(vector<int> &arr, int div) {
    int sum = 0;

    for(int i = 0; i < arr.size(); i++) {
        sum += (arr[i] + div - 1) / div;   // integer ceil trick
    }

    return sum;
}

int smallestDivisor(vector<int>& arr, int limit) {

    int n = arr.size();
    if(n > limit) return -1;   // impossible case

    int low = 1;
    int high = *max_element(arr.begin(), arr.end());

    while(low <= high) {
        int mid = low + (high - low) / 2;

        if(sumByD(arr, mid) <= limit) {
            high = mid - 1;   // try smaller divisor
        }
        else {
            low = mid + 1;    // increase divisor
        }
    }

    return low;
}
```

### capacity to ship packages within d days
```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to calculate days required for a given capacity
int calculateDays(vector<int>& weights, int capacity) {
    int days = 1;      // start with day 1
    int load = 0;

    for(int i = 0; i < weights.size(); i++) {

        // If adding this package exceeds capacity → next day
        if(load + weights[i] > capacity) {
            days++;
            load = weights[i];   // start new day with current weight
        }
        else {
            load += weights[i];
        }
    }

    return days;
}

int shipWithinDays(vector<int>& weights, int d) {

    int low = *max_element(weights.begin(), weights.end()); // minimum capacity
    int high = accumulate(weights.begin(), weights.end(), 0); // maximum capacity

    while(low <= high) {
        int mid = (low + high) / 2;

        int requiredDays = calculateDays(weights, mid);

        if(requiredDays <= d) {
            high = mid - 1;   // try smaller capacity
        }
        else {
            low = mid + 1;    // need bigger capacity
        }
    }

    return low;  // minimum valid capacity
}
```

* **binary search method**
```cpp
#include <bits/stdc++.h>
using namespace std;

int findDays(vector<int> &weights, int cap) {

    int days = 1;
    int load = 0;

    for(int i = 0; i < weights.size(); i++) {

        if(load + weights[i] > cap) {
            days++;
            load = weights[i];
        }
        else {
            load += weights[i];
        }
    }

    return days;
}

int leastWeightCapacity(vector<int> &weights, int d) {

    int low = *max_element(weights.begin(), weights.end());
    int high = accumulate(weights.begin(), weights.end(), 0);

    while(low <= high) {

        int mid = (low + high) / 2;

        int numberOfDays = findDays(weights, mid);

        if(numberOfDays <= d) {
            high = mid - 1;   // try smaller capacity
        }
        else {
            low = mid + 1;    // need bigger capacity
        }
    }

    return low;
}
```

### kth missing positive number
* linear method 
```cpp
    int findKthPositive(vector<int>& arr, int k) {
        
        for(int i = 0; i < arr.size(); i++) {
            if(arr[i] <= k) {
                k++;
            }
            else {
                break;
            }
        }

        return k;
    }
```

* binary method
```cpp
int missingK(vector<int> vec, int n, int k) {
    int low = 0, high = n - 1;
    while(low <= high) {
        int mid = (low + high) / 2;
        int missing = vec[mid] - (mid + 1);
        if(missing < k) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return k + high + 1;
}
```













## aggressive cows

* linear 
```cpp
bool canPlace(vector<int> &stalls, int dist, int cows) {
    int count = 1, last = stalls[0];

    for(int i = 1; i < stalls.size(); i++) {
        if(stalls[i] - last >= dist) {
            count++;
            last = stalls[i];
        }
        if(count >= cows) return true;
    }
    return false;
}

int aggressiveCowsLinear(vector<int> &stalls, int cows) {
    sort(stalls.begin(), stalls.end());

    int maxDist = stalls.back() - stalls.front();

    for(int d = 1; d <= maxDist; d++) {
        if(!canPlace(stalls, d, cows))
            return d - 1;
    }

    return maxDist;
}
```

* binary
```cpp
int aggressiveCows(vector<int> &stalls, int cows) {
    sort(stalls.begin(), stalls.end());

    int low = 1;
    int high = stalls.back() - stalls.front();
    int ans = 0;

    while(low <= high) {
        int mid = (low + high) / 2;

        if(canPlace(stalls, mid, cows)) {
            ans = mid;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return ans;
}
```


### book allocation problem
```cpp
#include <bits/stdc++.h>
using namespace std;

int countStudents(vector<int> &arr, int pages) {
    int students = 1;
    long long pagesStudent = 0;

    for (int i = 0; i < arr.size(); i++) {
        if (pagesStudent + arr[i] <= pages) {
            pagesStudent += arr[i];
        }
        else {
            students += 1;
            pagesStudent = arr[i];
        }
    }
    return students;
}

int findPages(vector<int> &arr, int n, int m) {
    if (m > n) return -1;

    int low = *max_element(arr.begin(), arr.end());
    int high = accumulate(arr.begin(), arr.end(), 0);

    while (low <= high) {
        int mid = (low + high) / 2;
        int students = countStudents(arr, mid);

        if (students > m) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return low;
}
```

## split array largest sums
```cpp
int countSubarrays(vector<int>& nums, int maxSum) {
    int subarrays = 1;
    long long sum = 0;

    for(int i = 0; i < nums.size(); i++) {
        if(sum + nums[i] <= maxSum) {
            sum += nums[i];
        }
        else {
            subarrays++;
            sum = nums[i];
        }
    }

    return subarrays;
}
```


## painter's partition
```cpp
int countStudents(vector<int>& arr, int pages) {
    int students = 1;
    long long pagesStudent = 0;

    for (int i = 0; i < arr.size(); i++) {
        if (pagesStudent + arr[i] <= pages) {
            pagesStudent += arr[i];
        }
        else {
            students += 1;
            pagesStudent = arr[i];
        }
    }
    return students;
}

int findPages(vector<int>& arr, int n, int m) {
    if (m > n) return -1;

    int low = *max_element(arr.begin(), arr.end());
    int high = accumulate(arr.begin(), arr.end(), 0);

    while (low <= high) {
        int mid = (low + high) / 2;
        int students = countStudents(arr, mid);

        if (students > m) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return low;
}

int findLargestMinDistance(vector<int> &boards, int k) {
    return findPages(boards, boards.size(), k);
}
```


## minimize max distance to gas station

* brute 
```cpp
double median(vector<int>& a, vector<int>& b) {
    vector<int> arr3;

    int n1 = a.size(), n2 = b.size();
    int i = 0, j = 0;

    // merge both arrays
    while (i < n1 && j < n2) {
        if (a[i] < b[j])
            arr3.push_back(a[i++]);
        else
            arr3.push_back(b[j++]);
    }

    while (i < n1)
        arr3.push_back(a[i++]);

    while (j < n2)
        arr3.push_back(b[j++]);

    int n = n1 + n2;

    if (n % 2 == 1) {
        return arr3[n / 2];
    }

    return (arr3[n/2] + arr3[n/2 - 1]) / 2.0;
}
```

* optimal 
```cpp
double median(vector<int>& a, vector<int>& b) {
    int n1 = a.size(), n2 = b.size();

    int i = 0, j = 0;
    int n = n1 + n2;

    int ind2 = n / 2;
    int ind1 = ind2 - 1;

    int cnt = 0;
    int ind1el = -1, ind2el = -1;

    while (i < n1 && j < n2) {

        if (a[i] < b[j]) {
            if (cnt == ind1) ind1el = a[i];
            if (cnt == ind2) ind2el = a[i];
            cnt++;
            i++;
        } 
        else {
            if (cnt == ind1) ind1el = b[j];
            if (cnt == ind2) ind2el = b[j];
            cnt++;
            j++;
        }
    }

    while (i < n1) {
        if (cnt == ind1) ind1el = a[i];
        if (cnt == ind2) ind2el = a[i];
        cnt++;
        i++;
    }

    while (j < n2) {
        if (cnt == ind1) ind1el = b[j];
        if (cnt == ind2) ind2el = b[j];
        cnt++;
        j++;
    }

    if (n % 2 == 1) return ind2el;

    return (ind1el + ind2el) / 2.0;
}
```

## median of 2 sorted arrays
```cpp
double median(vector<int>& a, vector<int>& b) {
    int n1 = a.size(), n2 = b.size();

    int i = 0, j = 0;
    int n = n1 + n2;

    int ind2 = n / 2;
    int ind1 = ind2 - 1;

    int cnt = 0;
    int ind1el = -1, ind2el = -1;

    while (i < n1 && j < n2) {

        if (a[i] < b[j]) {
            if (cnt == ind1) ind1el = a[i];
            if (cnt == ind2) ind2el = a[i];
            cnt++;
            i++;
        } 
        else {
            if (cnt == ind1) ind1el = b[j];
            if (cnt == ind2) ind2el = b[j];
            cnt++;
            j++;
        }
    }

    while (i < n1) {
        if (cnt == ind1) ind1el = a[i];
        if (cnt == ind2) ind2el = a[i];
        cnt++;
        i++;
    }

    while (j < n2) {
        if (cnt == ind1) ind1el = b[j];
        if (cnt == ind2) ind2el = b[j];
        cnt++;
        j++;
    }

    if (n % 2 == 1) return ind2el;

    return (ind1el + ind2el) / 2.0;
}
```

## kth element of 2 sorted arrays
```cpp
#include <bits/stdc++.h>
using namespace std;

int kthElement(vector<int> &a, vector<int>& b, int n1, int n2, int k) {

    if (n1 > n2) 
        return kthElement(b, a, n2, n1, k);

    int low = max(0, k - n2);
    int high = min(k, n1);

    while (low <= high) {

        int mid1 = (low + high) >> 1;
        int mid2 = k - mid1;

        int l1 = INT_MIN, l2 = INT_MIN;
        int r1 = INT_MAX, r2 = INT_MAX;

        if (mid1 < n1) r1 = a[mid1];
        if (mid2 < n2) r2 = b[mid2];

        if (mid1 - 1 >= 0) l1 = a[mid1 - 1];
        if (mid2 - 1 >= 0) l2 = b[mid2 - 1];

        if (l1 <= r2 && l2 <= r1) {
            return max(l1, l2);
        }
        else if (l1 > r2) {
            high = mid1 - 1;
        }
        else {
            low = mid1 + 1;
        }
    }

    return 0;
}
```

# BS on 2D Arrays

## row with maximum numbers of ones
```cpp
#include <bits/stdc++.h>
using namespace std;

int lowerBound(vector<int> arr, int n, int x) {

    int low = 0, high = n - 1;
    int ans = n;

    while (low <= high) {

        int mid = (low + high) / 2;

        if (arr[mid] >= x) {
            ans = mid;
            high = mid - 1;
        } 
        else {
            low = mid + 1;
        }
    }

    return ans;
}

int rowWithMax1s(vector<vector<int>> &matrix, int n, int m) {

    int cnt_max = 0;
    int index = -1;

    // n * log(m)
    for (int i = 0; i < n; i++) {

        int cnt_ones = m - lowerBound(matrix[i], m, 1);

        if (cnt_ones > cnt_max) {
            cnt_max = cnt_ones;
            index = i;
        }
    }

    return index;
}
```

## search in 2D matrix I
```cpp
#include <bits/stdc++.h>
using namespace std;

bool searchMatrix(vector<vector<int>>& mat, int target) {

    int n = mat.size();
    int m = mat[0].size();

    int low = 0, high = n * m - 1;

    while (low <= high) {

        int mid = (low + high) / 2;

        int row = mid / m;
        int col = mid % m;

        if (mat[row][col] == target) 
            return true;

        else if (mat[row][col] < target) 
            low = mid + 1;

        else 
            high = mid - 1;
    }

    return false;
}
```

## search in 2D matrix II
```cpp
#include <bits/stdc++.h>
using namespace std;

bool searchElement(vector<vector<int>>& mat, int target) {
    int n = mat.size();
    int m = mat[0].size();

    int row = 0, col = m - 1;

    while (row < n && col >= 0) {
        if (mat[row][col] == target) 
            return true;
        else if (mat[row][col] < target) 
            row++;
        else 
            col--;
    }

    return false;
}
```

## find peak elements II
```cpp
#include <bits/stdc++.h>
using namespace std;

int findMaxIndex(vector<vector<int>>& mat, int n, int m, int col) {
    int maxValue = -1;
    int index = -1;

    for (int i = 0; i < n; i++) {
        if (mat[i][col] > maxValue) {
            maxValue = mat[i][col];
            index = i;
        }
    }
    return index;
}

vector<int> findPeakGrid(vector<vector<int>>& mat) {
    int n = mat.size();
    int m = mat[0].size();

    int low = 0, high = m - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        int maxRowIndex = findMaxIndex(mat, n, m, mid);

        int left = (mid - 1 >= 0) ? mat[maxRowIndex][mid - 1] : -1;
        int right = (mid + 1 < m) ? mat[maxRowIndex][mid + 1] : -1;

        if (mat[maxRowIndex][mid] > left && mat[maxRowIndex][mid] > right) {
            return {maxRowIndex, mid};
        }
        else if (mat[maxRowIndex][mid] < left) {
            high = mid - 1;
        }
        else {
            low = mid + 1;
        }
    }

    return {-1, -1};
}
```

## median in a row wise sorted matrix 
```cpp
#include <bits/stdc++.h>
using namespace std;

// Upper Bound: first index where element > x
int upperBound(vector<int> &arr, int x, int n) {
    int low = 0, high = n - 1;
    int ans = n;

    while (low <= high) {
        int mid = (low + high) / 2;

        if (arr[mid] > x) {
            ans = mid;
            high = mid - 1;
        } 
        else {
            low = mid + 1;
        }
    }
    return ans;
}

// Count elements <= x
int countSmallEqual(vector<vector<int>> &matrix, int n, int m, int x) {
    int cnt = 0;

    for (int i = 0; i < n; i++) {
        cnt += upperBound(matrix[i], x, m);
    }

    return cnt;
}

// Find median
int median(vector<vector<int>> &matrix, int n, int m) {

    int low = INT_MAX, high = INT_MIN;

    // Find range
    for (int i = 0; i < n; i++) {
        low = min(low, matrix[i][0]);
        high = max(high, matrix[i][m - 1]);
    }

    int req = (n * m) / 2;

    // Binary Search on Answer
    while (low <= high) {
        int mid = (low + high) / 2;

        int smallEqual = countSmallEqual(matrix, n, m, mid);

        if (smallEqual <= req)
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}
```






