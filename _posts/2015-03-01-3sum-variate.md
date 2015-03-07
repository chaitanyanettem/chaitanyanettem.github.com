---
layout: post
title: 3-Sum and its myriad avatars
date: 2015-03-01 12:20
permalink: 3sum-variate
summary: The 3-Sum is a popular programming puzzle and is presented to people in many different forms.
categories: interview-prep
---

The 3-Sum is a popular programming puzzle and is presented to people in many different forms. Here I will endeavor to dissect its more popular versions.

###Let's start with the 2-Sum

The question is thus:

<div class="bg-light-gray rounded-para">

<p>Given an array of integers, find two numbers such that they add up to a specific target number.</p>

<p>The function twoSum() should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.</p>

<p>You may assume that each input would have exactly one solution.</p>

<p>Input: numbers = {2, 7, 11, 15}, target = 9</p>

<p>Output: index1 = 1, index2 = 2</p>
</div>

<br/>
Here you have an array of numbers and you have to find out if any two of them sum to a given target number. The most obvious way to solve it is to brute force your way to sum all possible combinations:

```C++
class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        vector<int> solution;
        for ( int i=0; i<numbers.size()-1; i++ ) 
            for ( int j=i+1; j<numbers.size(); j++ ) 
                if ( numbers[i]+numbers[j] == target ) {
                    solution.push_back(i+1);
                    solution.push_back(j+1);
                    return solution;
                }
    }
};
```

Obviously we can do better than that in terms of time. A better way is to use a hashtable/map. (This is something a professor once told me: When in doubt use a hashtable :).

So, we can use a C++ map to store each number in the map when we first encounter it. Simultaneously we can check if the target minus that number already exists in the map. If it does, bingo!

```C++
class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        map<int, int> hash;
        vector<int> result;
        
        for (int i=0; i<numbers.size(); i++) {
            if (hash.find(target - numbers[i]) != hash.end()) {
                if (i + 1< hash[target - numbers[i]]) {
                    result.push_back(i+1);
                    result.push_back(hash[target-numbers[i]]);
                }
                else {
                    result.push_back(hash[target-numbers[i]]);
                    result.push_back(i+1);
                }
            }
            else
                hash[numbers[i]] = i+1;
        }
        return result;
    }
};
```
To be continued...

