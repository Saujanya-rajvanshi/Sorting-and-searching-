# Sorting-and-searching-

#### bubble sort 
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
