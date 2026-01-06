# Sorting-and-searching-
### index
- [bubble sort](#bubble-sort)
- [insertion sort](#insertion-sort)
- [selection sort](#selection-sort)
- [merge sort](#merge-sort)
- [quick sort](#quick-sort)
- [heap sort](#heap-sort)
- [comparison](#comparison)


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
#include <bits/stdc++.h>
using namespace std;

int partition(vector<int> &arr, int low, int high) {
    int pivot = arr[low];
    int i = low;
    int j = high;

    while (i < j) {
        while (arr[i] <= pivot && i <= high - 1)
            i++;

        while (arr[j] > pivot && j >= low + 1)
            j--;

        if (i < j)
            swap(arr[i], arr[j]);
    }

    swap(arr[low], arr[j]);
    return j;
}

void qs(vector<int> &arr, int low, int high) {
    if (low < high) {
        int pIndex = partition(arr, low, high);
        qs(arr, low, pIndex - 1);
        qs(arr, pIndex + 1, high);
    }
}

int main() {
    vector<int> arr = {5, 2, 9, 1, 5, 6};

    qs(arr, 0, arr.size() - 1);

    for (int x : arr)
        cout << x << " ";
    return 0;
}
```
## comparison 

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
