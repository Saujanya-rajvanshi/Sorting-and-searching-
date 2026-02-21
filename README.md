# Sorting-and-searching-
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
  
###### searching 


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













# searching 

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

### **Binary Search[1D,2D,Array,Search Space]**

#### BS on 1D Arrays

- [binary search to find x in sorted array](#binary-search-to-find-x-in-sorted-array)
- [implement lower bound](#implement-lower-bound)
- [implement upper bound](#implement-upper-bound)
- [search insert position](#search-insert-position)
- [floor/ceil in sorted array](#floorceil-in-sorted-array)
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




