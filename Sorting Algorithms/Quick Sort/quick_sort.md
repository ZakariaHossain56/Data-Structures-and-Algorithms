## QUICK SORT
- It's a **divide and conquer** algorithm that picks an element as a pivot and partitions the given array around the picked pivot by placing the pivot in its correct position in the sorted array.
- It is efficient on **large data sets**.
- Fastest general purpose algorithm for large data when **stability** is not required.
- It is **not a stable** sort, meaning that if two elements have the same key, their relative order will not be preserved in the sorted output in case of quick sort, because here we are swapping elements according to the pivot’s position (without considering their original positions).
### How it works
- Choose a pivot(first, last, mid or any elements).
- Rearrange the array so that all elements smaller than the pivot will be on the left and all elements greater than the pivot will be on the right.
- Recursively apply the same process for the partitioned subarrays.
<p align="center"><img src="quick_sort.png" width="400" height="220"></p>

### Algorithm
- Choose the last element as pivot. Initialize `i=-1` and `j=0`.
- If `arr[j]<pivot`, increment `i` and swap `arr[i]` and `arr[j]`. Increment `j`.
- Else if `arr[j]>=pivot`, no swap needed, increment `j`.
<p align="center"><img src="quick_sort1.png" width="400" height="220"></p>
<p align="center"><img src="quick_sort2.png" width="400" height="220"></p>
<p align="center"><img src="quick_sort3.png" width="400" height="220"></p>
<p align="center"><img src="quick_sort4.png" width="400" height="220"></p>
<p align="center"><img src="quick_sort5.png" width="400" height="220"></p>
<p align="center"><img src="quick_sort6.png" width="400" height="220"></p>

### Code
```cpp
#include <bits/stdc++.h>
using namespace std;
int getPivotIndex(vector<int> &v, int low, int high){
	int pivot = v[high];    //choose the last element as pivot
	int i = low-1;
	for(int j=low;j<high;j++){
		if(v[j] < pivot){
			i++;
			swap(v[i], v[j]);
		}
	}
	swap(v[i+1], v[high]);
	return i+1;
}
void quickSort(vector<int> &v, int low, int high){
	if(low < high){
		int pivot_Index = getPivotIndex(v, low, high);  //get the pivot index
		quickSort(v, low, pivot_Index-1);   //recursive call for left subarray
		quickSort(v, pivot_Index+1, high);  //recursive call for right subarray
	}
}
int main(){
	vector<int> v = {10, 7, 8, 9, 1, 5};
	quickSort(v, 0, v.size()-1);
	cout<<"Sorted elements: ";
	for(int i=0;i<v.size();i++){
		cout<<v[i]<<" ";
	}
	cout<<endl;
}
```
### Complexity Analysis
#### Time Complexity
- **Best case:** `O(nlogn)`, when the pivot element divides the array into two equal halves.
- **Average case:** `O(nlogn)`, when the pivot element divides the array into two halves, not necessarily equal.
- **Worst case:** `O(n^2)`, when the array is sorted(when the smallest or the largest element is choosen).
#### Space Complexity
- No space needed for input array, space complexity arises due to the recursion stack.
- **Best case:** `O(logn)`, when the pivot element divides the array into two equal halves.
- **Average case:** `O(logn)`, when the pivot element divides the array into two halves, not necessarily equal.
- **Worst case:** `O(n)`, due to unbalanced partitioning causing a skewed recursion tree that requires a call stack of size `O(n)`.
<p align="center"><img src="quick_sort_complexity.png" width="450" height="220"></p>

### Q&A
Q1. Which of the following can improve Quick Sort’s performance in the worst case?
	a. Randomized pivot selection
	b. Always choosing the first element as the pivot
	c. Sorting a sorted array
	d. Using a stack-based approach
	Answer:
	a. **Randomized pivot selection**

Q2. What is the primary advantage of Quick Sort over Merge Sort?
	a. Stability
	b. Worst-case performance
	c. Space efficiency
	d. Simplicity of implementation
	Answer:
	c. **Space efficiency**

Q3. In Quick Sort, if the pivot divides the array into two equal halves at every step, the depth of recursion will be:
	a. O(n)
	b. O(log n)
	c. O(n²)
	d. O(1)
	Answer:
	b. **O(log n)**

Q4. Which of the following modifications is NOT used to optimize Quick Sort?
	a. Median-of-three pivot selection
	b. Switching to Insertion Sort for small subarrays
	c. Randomized pivot selection
	d. Using an auxiliary array for partitioning
	Answer:
	d. **Using an auxiliary array for partitioning**

Q5. Quick Sort is typically implemented:
	a. Iteratively using a stack
	b. Recursively
	c. Both iteratively and recursively
	d. Using only a loop
	Answer:
	c. **Both iteratively and recursively**

Q6. If Quick Sort is implemented using a loop instead of recursion, what is used to simulate the recursive calls?
	a. Queue
	b. Array
	c. Stack
	d. Linked List
	Answer:
	c. **Stack**

Q7. Why is Quick Sort generally faster than other sorting algorithms in practical scenarios?
	a. It always uses O(1) space
	b. It avoids recursion
	c. It has better cache performance due to in-place sorting
	d. It does not use pivot selection
	Answer:
	c. **It has better cache performance due to in-place sorting**

Q8. What happens in Quick Sort when all elements in the array are identical?
	a. Best-case time complexity is achieved
	b. Average-case time complexity is achieved
	c. Worst-case time complexity is achieved
	d. Time complexity is O(1)
	Answer:
	c. **Worst-case time complexity is achieved**

Q9. Quick Sort’s performance can be improved by:
	a. Choosing the largest element as the pivot
	b. Sorting an already sorted array
	c. Choosing the median-of-three as the pivot
	d. Reducing the number of comparisons
	Answer:
	c. **Choosing the median-of-three as the pivot**

Q10. Which of the following is true about the partitioning step in Quick Sort?
	a. The pivot is always placed at the first position of the array.
	b. The pivot element is placed in its final sorted position.
	c. The pivot is not included in the partitioned subarrays.
	d. The partitioning step merges two sorted arrays.
	Answer:
	b. **The pivot element is placed in its final sorted position.**