# Radix-Sort-Algorithm

<i><b>
Radix Sort is a linear sorting algorithm that sorts elements by processing them digit by digit. It is an efficient sorting algorithm for integers or strings with fixed-size keys. 

Rather than comparing elements directly, Radix Sort distributes the elements into buckets based on each digit’s value. By repeatedly sorting the elements by their significant digits, from the least significant to the most significant, Radix Sort achieves the final sorted order.
<b/>
</i>

- Radix Sort Algorithm
The key idea behind Radix Sort is to exploit the concept of place value. It assumes that sorting numbers digit by digit will eventually result in a fully sorted list. Radix Sort can be performed using different variations, such as Least Significant Digit (LSD) Radix Sort or Most Significant Digit (MSD) Radix Sort.


# How does Radix Sort Algorithm work?

To perform radix sort on the array [170, 45, 75, 90, 802, 24, 2, 66], we follow these steps:

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230609164537/Radix-Sort.png" width='400'>
</div>

<h2>Step 1: </h2> Find the largest element in the array, which is 802. It has three digits, so we will iterate three times, once for each significant place.


<h2>Step 2: </h2> Sort the elements based on the unit place digits (X=0). We use a stable sorting technique, such as counting sort, to sort the digits at each significant place. It’s important to understand that the default implementation of counting sort is unstable i.e. same keys can be in a different order than the input array. To solve this problem, We can iterate the input array in reverse order to build the output array. This strategy helps us to keep the same keys in the same order as they appear in the input array.

<h2>Sorting based on the unit place:</h2>

- Perform counting sort on the array based on the unit place digits.
- The sorted array based on the unit place is [170, 90, 802, 2, 24, 45, 75, 66].

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230609164536/Radix-Sort--1.png" width='400'>
</div>



<h2>Step 3: </h2> Sort the elements based on the tens place digits.

Sorting based on the tens place:

- Perform counting sort on the array based on the tens place digits.
- The sorted array based on the tens place is [802, 2, 24, 45, 66, 170, 75, 90].



<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230609164535/Radix-Sort--2.png" width='400'>
</div>


<h2>Step 4: </h2> Sort the elements based on the hundreds place digits.


Sorting based on the hundreds place:


- Perform counting sort on the array based on the hundreds place digits.
- The sorted array based on the hundreds place is [2, 24, 45, 66, 75, 90, 170, 802].

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230609164535/Radix-Sort--3.png" width='400'>
</div>

<h2>Step 5: </h2> The array is now sorted in ascending order.

The final sorted array using radix sort is [2, 24, 45, 66, 75, 90, 170, 802].

<div align="center">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/20230609164534/Radix-Sort--4.png" width='400'>
</div>


# Below is the implementation for the above illustrations:

```
// C++ implementation of Radix Sort

#include <iostream>
using namespace std;

// A utility function to get maximum
// value in arr[]
int getMax(int arr[], int n)
{
    int mx = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > mx)
            mx = arr[i];
    return mx;
}

// A function to do counting sort of arr[]
// according to the digit
// represented by exp.
void countSort(int arr[], int n, int exp)
{

    // Output array
    int output[n];
    int i, count[10] = { 0 };

    // Store count of occurrences
    // in count[]
    for (i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    // Change count[i] so that count[i]
    // now contains actual position
    // of this digit in output[]
    for (i = 1; i < 10; i++)
        count[i] += count[i - 1];

    // Build the output array
    for (i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    // Copy the output array to arr[],
    // so that arr[] now contains sorted
    // numbers according to current digit
    for (i = 0; i < n; i++)
        arr[i] = output[i];
}

// The main function to that sorts arr[]
// of size n using Radix Sort
void radixsort(int arr[], int n)
{

    // Find the maximum number to
    // know number of digits
    int m = getMax(arr, n);

    // Do counting sort for every digit.
    // Note that instead of passing digit
    // number, exp is passed. exp is 10^i
    // where i is current digit number
    for (int exp = 1; m / exp > 0; exp *= 10)
        countSort(arr, n, exp);
}

// A utility function to print an array
void print(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 170, 45, 75, 90, 802, 24, 2, 66 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    radixsort(arr, n);
    print(arr, n);
    return 0;
}
```

# Output:

```
2 24 45 66 75 90 170 802
```

# Complexity: 

- Time Complexity: O(d * (n + b))
- Space complexity:  O(n + b)















