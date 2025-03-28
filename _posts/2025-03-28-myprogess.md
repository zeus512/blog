---
layout: post
title:  "Daily progess"
author: Charan 
categories: [ Daily progress ]
---

26-03-2025
tuf -  sortings/algorithms all 5 
Selection sort
Bubble sort
Insertion sort
Merge sort
Quick sort 
All basic algorithms have mostly no changes.

-Arrays FAQ (medium,hard)
Two sum
 Given an array of integers nums and an integer target. Return the indices(0 - indexed) of two elements in nums such that they add up to target.
Each input will have exactly one solution, and the same element cannot be used twice. Return the answer in non-decreasing order.
  Using brute force two loops. o(n2)
  Using while loop (complex version of brute force) 0(n2)
  HashMap (target - sum) and then checking. 0()
3 sum 
  Given an integer array nums. Return all triplets such that:
i != j, i != k, and j != k
nums[i] + nums[j] + nums[k] == 0.
Notice that the solution set must not contain duplicate triplets. One  element can be a part of multiple triplets. The output and the triplets can be returned in any order.
Using brute force (3 loops stop when == 0)  0(n3)
Sorting and then using loops to get the sum using i,left,right; using while loop till left>right while checking for sum and going through it 

Sort an array of 0s 1s 2s
Given an array nums consisting of only 0, 1, or 2. Sort the array in non-decreasing order. The sorting must be done in-place, without making a copy of the original array.   
 Using Arrays.sort 0(n log n)
Something called Dutch National Flag Algorithm which is similar to quick sort  0(n)

Majority element-1
Given an integer array nums of size n, return the majority element of the array.
The majority element of an array is an element that appears more than n/2 times in the array. The array is guaranteed to have a majority element.
Using Hashmap 0(n).

Majority element-2
Given an integer array nums of size n. Return all elements which appear more than n/3 times in the array. The output can be returned in any order.
  Same as Majority element-1 but n/3 0(n).

LeetCode 
7. Reverse Integer
Usual method with some constraints 0(logn)
8. String to Integer (atoi)
 Conditions and checking them accordingly 0(n)

27-03-2025
LeetCode 
12. Integer to Roman
Giving the string values and dividing them till the end. 0(1)
15. 3Sum
Yesterday's 2nd one. same
16. 3Sum Closest
 Same as above but different conditions
18. 4Sum
Mentioned below


TUF 
Kadane's Algorithm
 Given an integer array nums, find the subarray with the largest sum and return the sum of the elements present in that subarray.
A subarray is a contiguous non-empty sequence of elements within an array
 Normal loop of max sum 0(n) 
4 sum
     Given an integer array nums and an integer target. Return all quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:
·      a, b, c, d are all distinct valid indices of nums.
·      nums[a] + nums[b] + nums[c] + nums[d] == target.
Notice that the solution set must not contain duplicate quadruplets. One element can be a part of multiple quadruplets. The output and the quadruplets can be returned in any order.
 4 loops 0(n4)
Using similar procedure as 3 sum 0(n3)
Rotate Matrix by 90 deg
Given an N * N 2D integer matrix, rotate the matrix by 90 degrees clockwise.
The rotation must be done in place, meaning the input 2D matrix must be modified directly.
   1 Using double loop to copy and paste 0(n2)+0(n2)
Pascal's Triangle 1.
 Given two integers r and c, return the value at the rth row and cth column in a Pascal's Triangle.
        In Pascal's triangle:
The first row has one element with a value of 1.
Each row has one more element in it than its previous row.
The value of each element is equal to the sum of the elements directly above it when arranged in a triangle format.
Using the formula ncr= n!/r!*n-r!   0(c)
Pascal's Triangle 2
 Given an integer r, return all the values in the rth row in Pascal's Triangle in correct order.
In Pascal's triangle:
The first row has one element with a value of 1.
Each row has one more element in it than its previous row.
The value of each element is equal to the sum of the elements directly above it when arranged in a triangle format.
Using formula 0(r)
Pascal's Triangle 3
Given an integer n, return the first n rows of Pascal's triangle.
In Pascal's triangle:
The first row has one element with a value of 1.
Each row has one more element in it than its previous row.
The value of each element is equal to the sum of the elements directly above it when arranged in a triangle format.
 Same as pascal 2 just addition of list and recursion 0(n2)
  
   
28-03-2025

TUF
 leaders in the array.
  Given an integer array nums, return a list of all the leaders in the array.
A leader in an array is an element whose value is strictly greater than all elements to its right in the given array. The rightmost element is always a leader. The elements in the leader array must appear in the order they appear in the nums array.
  1 using reverse loop and checking for maximum 0(n)
Print the Matrix in spiral 
 Given an M * N matrix, print the elements in a clockwise spiral manner. Return an array with the elements in the order of their appearance when printed in a spiral manner.
                          1. Going through it as the perimeter from one end to another 0(m*n)
Find Missing Repeating Numbers
 Given an integer array nums of size n containing values from [1, n] and each value appears exactly once in the array, except for A, which appears twice and B which is missing.
Return the values A and B, as an array of size 2, where A appears in the 0-th index and B in the 1st index.
Using a hashset and formula 0(n) missing=expected sum−(actual sum−repeating number)
Count Inversions
Given an integer array nums. Return the number of inversions in the array.
Two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.
It indicates how close an array is to being sorted.
A sorted array has an inversion count of 0.
An array sorted in descending order has maximum inversion.
