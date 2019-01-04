---
title: 	"Insertion Sort in C"
date: 	2019-01-04
tags: 	[algorithms]
---

Insertion sort is a simple algorithm that builds the final sorted array (or list) one item at a time. It is much less 
efficient on large lists than other sorting algorithm like quicksort, heapsort, or merge sort. However, insertion sort 
provides several advantageds:

* Simple implementation
* Efficient for quite small data sets.
* Adaptive, i.e., efficient for data sets that are already substantially sorted: the time complexity is O(nk) when each 
element in the input is no more than k places away from its sorted position.
* In-place; i.e., only requires a constant amount O(1) of additional memory space
* Online; i.e., can sort a list as it receives an element

Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list. At each 
iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted 
list, and insert it there. It repeats untill no input element remain. At each array position, it checks the value there 
aganist the largest value in the sorted list (which happens to be previous element to it). If larger, it leaves the 
element in palce and moves to the next element. If smaller, it finds the correct position within the sorted list, 
shifts all the larger values up to make a space, and insert into that correct position.

1. Worst case time complexity O(n^2), swaps
2. Best case time complexity O(n) comparisons, O(1) swaps
3. Average case time complexity O(n^2), swaps
4. Worst case space complexity O(n)

Now that we have completed the theoritical part, lets write the C code for Insertion sort. 

```C
/*
* brief: Run insertion sort on the array pointed by pArr
* param: Pointer to an int array to be sorted, and number of elements in the array.
* return: None
*/

void insertionSort(int * pArr, int size)
{
	int i = 1;
	int * pData = pArr;
	
	for(i; i < size; i++)
	{
		if(*(pArr + i) < *(pData))
		{
			int j = i-1;
			int k = i;

			while(j >= 0)
			{
				if(*(pArr+ j) > *(pArr + k))
				{
					// Swap the two data element 
					int swp = *(pArr + j);
					*(pArr + j) = *(pArr + k);
					*(pArr + k) = swp;
					j--;
					k--;
				}
				else
				{
					break;
				}
			}
		}

		// this portion display the array with each iteration of the process
		for(int n = 0; n < size; n++)
		{
		    printf("%d \t", *(pArr + n));
		}
        	printf("\n");

		pData++;
	}
}

```

Now to test the above code, we can write a simple test case like this.

```C
int main(void)
{
	int arr[] = {3, 4, 1, 6, 0, 8, 2, 10};
	int size = 8;

	int i = 0;

	printf("The original array is \n");
	for(i; i < size; i++)
	{
		printf("%d \t", arr[i]);
	}

	printf("\n");

    	printf("\nStarting Insertion Sort \n");
	insertionSort(arr, size);

	printf("\nThe sorted array is \n");
	for(i = 0; i < size; i++)
	{
		printf("%d \t", arr[i]);
	}

	printf("\n");

	return 0;
}

```

[Reference](https://en.wikipedia.org/wiki/Insertion_sort)
