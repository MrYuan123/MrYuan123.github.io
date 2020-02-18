---
layout:     post
title:      "Leetcode Test Notes(1-20)"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-9-9 14：00
author:     "Leonard Yuan"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - Leetcode
    - Internship
    - Interview 
---

>pre
>
>This week, I start learn and solve questions in leetcode, my goal is that I will solve 150 questions until October. Meanwhile, I will use my blog to document the solutions and thinkings about these question. So, let's start it.


	Notice: we use python3 as coding language to deal with these problems.

## 5. Longest Palindromic Substring

this is a classic algorithm question, there are some solutions about this questions.

- Brute Force

This is the easiest solution, but cannot pass from leetcode because of running so much time, but I will give my codes as follows:

	# brute force
	class Solution:
	    def longestPalindrome(self, s):
	        if len(s) == 0:
	            return s
	        elif len(s) == 1:
	            return s
	        else:
	            substring = ''
	            for m in range(len(s)):
	                for n in range(m+1,len(s)+1):
	                    flag = self.whetherpa(s[m:n])
	                    if flag == 1 and len(s[m:n]) > len(substring):
	                        substring = s[m:n]

	            return substring

	    def whetherpa(self, m):
	        l = m[::-1]
	        if l == m:
	            return 1
	        else:
	            return 0

- Expand from a center

This is a effective solution, we can test a string from a center, if we find that the former word and the later one are same, we can define that this string are also a palindromic substring, thus, we can find the longest palindromic substring easily according to this principle. There is another issue we should care about, that is what kind of center we should choose. After observation, we can find there are two kinds of different centers, one is like 'a', 'b', and so on, another is a substring having two same words, like 'aa', 'ee', and so on. Here is the code:

	# center way
	class Solution:
	    def longestPalindrome(self, s):
	        substring = ''
	        for m in range(len(s)):
	            returnstring = self.findstring(s,m,m)

	            if len(returnstring) > len(substring):
	                substring = returnstring

	            returnstring = self.findstring(s,m,m+1)
	            if len(returnstring) > len(substring):
	                substring = returnstring

	        return substring

	    def findstring(self, s, p, q):
	        while p > -1 and q <len(s) and s[p] == s[q]:
	            p -= 1
	            q += 1

	        return s[p+1:q]

- Dynamic Programming

......

- Manacher's Algorithm

......

## 6. ZigZag Conversion

- Just iterate the array

ZigZag conversion problem is likely that we arrange the existed array into new python lists, then we can join the elements in this list, and we will get the final array in the end. In my code, I use a variable to tag the direction of storing elements of the array into new list. I will give my code as follows:

	class Solution:
	    def convert(self, s, numRows):
	        if numRows == 1:
	            print(s)
	        nlist = [""]*numRows
	        flag = 0
	        dire = 0
	        for m in range(len(s)):
	            nlist[flag] = nlist[flag] + s[m]
	            if dire == 0:
	                if flag == numRows-1:
	                    dire = 1
	                    flag -= 1
	                else:
	                    flag += 1
	            else:
	                if flag == 0:
	                    dire = 0
	                    flag += 1
	                else:
	                    flag -= 1

	        return ''.join(nlist)

- Finding the characters

Another way to solve this problem is to find the characters of new array, so we can define certain equations to arrange the elements of given array into certain rows. We can find the equations in the solution page of this question in leetcode. Here is the link:

[the equation of this question](https://leetcode.com/problems/zigzag-conversion/solution/)

But my code has low effeciency, it is about 33.85%. Thus, I will take some further progress. I will give my code as follows:

	class Solution:
	    def convert(self, s, numRows):
	        if numRows == 1:
	            return s
	        nlist = ['']*numRows
	        for m in range(numRows):
	            if m == 0:
	                flag = 0
	                while flag*(2*numRows - 2) < len(s):
	                    nlist[m] = nlist[m] + s[flag*(2*numRows - 2)]
	                    flag += 1

	            elif m == numRows -1:
	                flag = 0
	                while (flag*(2*numRows - 2) + numRows - 1) < len(s):
	                    nlist[m] = nlist[m] + s[flag*(2*numRows - 2) + numRows - 1]
	                    flag += 1

	            else:
	                flag = 0
	                while (flag*(2*numRows-2) + m) < len(s) or ((flag + 1)*(2*numRows - 2) - m) < len(s):
	                    if (flag*(2*numRows-2) + m) < len(s):
	                        nlist[m] = nlist[m] + s[flag*(2*numRows-2) + m]
	                    if ((flag + 1)*(2*numRows - 2) - m) < len(s):
	                        nlist[m] = nlist[m] + s[(flag + 1)*(2*numRows - 2) - m]

	                    flag += 1

	        return ''.join(nlist)


## 9. Palindrome Number

This is an easy question, the best solution is that, we can choose elements from head and end, then we can compare them. If they are same, go on, or, return False. In the end, when head flag and end flag meet on certain position, we can define that this is a palindrome number, then return True. Here is the code:

	class Solution:
	    def isPalindrome(self, x):
	        x = str(x)
	        head = 0
	        end = len(x) -1
	        while end - head > 0:
	            if x[head] == x[end]:
	                head += 1
	                end -= 1
	            else:
	                return False

	        return True

## 10. Regular Expression Matching   

......

## 11. Container With Most Water   

- Brute Force

This is the easiest way, you should calculate the volume between two lines, then you can get the maximum volume. Omit the code.

- Two Pointer Approach

As we all know, if we want to find a container, which has the maximum volume, we must choose the longest lines to  make sure that we can get the container, having maximum volume. The video about this question on leetcode is pretty good, here is the link.

[vedio of 11th question](https://leetcode.com/problems/container-with-most-water/description/)

Here is the final code:

	class Solution:
	    def maxArea(self, height):
	        maxn = 0
	        head = 0
	        end = len(height) - 1
	        while end - head> 0:
	            print('%d : %d'% (head,end))
	            if (end - head) * min(height[head], height[end]) > maxn:
	                maxn = (end - head) * min(height[head], height[end])
	            if height[head] < height[end]:
	                head += 1
	            else:
	                end -= 1
	        return maxn


## 12. Integer to Roman

This is a pretty easy question, we can three lists to solve this question, every list contains the conversion of integers, the only thing we should do is to take the remainers to gain roman words, then we can join them into the final roman numbers. Here is the code:

	class Solution:
	    def intToRoman(self, num):
	        M = ['','M','MM','MMM']
	        C = ['','C','CC','CCC','CD','D','DC','DCC','DCCC','CM']
	        X = ['','X','XX','XXX','XL','L','LX','LXX','LXXX','XC']
	        I = ['','I','II','III','IV','V','VI','VII','VIII','IX']
	        return M[int(num/1000)] + C[int((num%1000)/100)] + X[int((num%100)/10)] + I[num%10]


## 13. Roman to Integer

First, I use the easiest way to fulfill this function, that is I build a dict to store as many as substring, when we achieve the comversion of Roman, the only thing we should do, is to match keys of the dict, then I can find the right number, and add it into sum variable. But it is of low effeicency, I just beats 5.18% by using this way. So I should make progress on my solution. Here is the code, which has the low effeciency.

	class Solution:
	    def romanToInt(self, s):
	        d = {'I':1, 'IV':4, 'V':5, 'IX':9, 'X':10, 'XL':40, 'L':50, 'XC':90, 'C':100, 'CD':400, 'D':500, 'CM':900, 'M':1000}
	        sum = 0
	        m = 0
	        while m < len(s) - 1:
	            if d.get(s[m] + s[m+1]):
	                sum = sum + d[s[m] + s[m+1]]
	                # print('2: '+ s[m] + s[m+1])
	                m += 2
	            else:
	                sum = sum + d[s[m]]
	                # print('1: '+ s[m])
	                m += 1
	        if m == len(s) - 1:
	            sum = sum + d[s[m]]
	        return sum

There is other way to improve the effeciency of my algorithm, that is we can reverse the array, then we can compare the late one with former one, if the former one is better, sum substracts the late one. If not, add it. Here is the code:

	class Solution:
	    def romanToInt(self, s):
	        d = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500,'M':1000}
	        sum = 0
	        s = s[::-1]
	        sum = d[s[0]]
	        for m in range(1,len(s)):
	            if d[s[m]] <d[s[m-1]]:
	                sum -= d[s[m]]
	            else:
	                sum += d[s[m]]
	        return sum

## 14. Longest Common Prefix

This is a pretty easy case, and the most important thing is that you should care about every possible situation, such as [], [""] and so on. We can use strs[0] as a standard array to match other arrays in strs, if they are not same, return, else, keep going. Here is the code as follows:

	class Solution:
	    def longestCommonPrefix(self, strs):
	        if len(strs) == 1:
	            return strs[0]
	        elif len(strs) == 0:
	            return ''
	        else:
	            rstr = ''
	            for m in range(len(strs[0])):
	                for l in strs[1:]:
	                    if strs[0][0:m+1] == l[0: m + 1]:
	                        pass
	                    else:
	                        return rstr
	                rstr = rstr + strs[0][m]

	            return rstr

## 15. 3Sum

This is an pretty interesting question, I first use two pointers, one from head, another from end, to start sort, but I found that there is an omition, thus I used Brute Force algorithm to solve this question. Although we can get final result, if we cannot pass from leetcode website because of the `Time Limit Exceeded`. Here is the code of brute force algorithm.

	class Solution:
	    def threeSum(self, nums):
	        if len(nums) == 0:
	            return []
	        else:
	            retset = []
	            nums = sorted(nums)
	            for m in range(0, len(nums) - 2):
	                for n in range( m + 1, len(nums) - 1):
	                    if 0 - (nums[m] + nums[n]) in nums[n+1 : len(nums)]:
	                        temp = sorted([nums[m], nums[n], 0 - nums[m] - nums[n]])
	                        if temp  not in retset:
	                            retset.append(temp)
	            return retset

We must make progress on my algorithm.

Here is the progress of this question, we use two pointers to fulfill my algorithm, and there are two loops, thus the complexity of my algorithm is O(n^2), but my solution still cannot pass the leetcode test system. So, keep going. Here is the code as following:

	class Solution:
	    def threeSum(self, nums):
	        if len(nums) == 0:
	            return []
	        else:
	            retset = []
	            nums = sorted(nums)
	            head = 0

	            while head < len(nums) - 2:
	                end = len(nums) - 1
	                while end > head + 1:
	                    if 0 - (nums[end] + nums[head])in nums[head + 1: end]:
	                        if [nums[head] ,0 - (nums[end] + nums[head]) , nums[end]] not in retset:
	                            print('1 %d : %d'%(nums[head], nums[end]))
	                            retset.append([nums[head] ,0 - (nums[end] + nums[head]) , nums[end]])
	                        end -= 1
	                    elif nums[end] - nums[head] > 0:
	                        print('1 %d : %d'%(nums[head], nums[end]))
	                        end -= 1
	                    else:
	                        break
	                head += 1
	            return retset


## 16. 3Sum Closest

The solution of this question is similar to question15, so I just give the code:

	class Solution:
	    def threeSumClosest(self, numbers, target):
	        numbers = sorted(numbers)
	        retans = None
	        for m in range(len(numbers)):
	            left = m + 1
	            right = len(numbers) - 1
	            while left < right:
	                sum = numbers[left] + numbers[right] + numbers[m]
	                if retans is None or abs(retans - target) >abs(sum - target):
	                    retans = sum
	                if sum <target:
	                    left += 1
	                else:
	                    right -= 1
	        return retans

## 17. Letter Combinations of a Phone Number

This is also an easy question, we can use three loops to solve this question. Here is the code:

	class Solution:
	    def letterCombinations(self, digits):
	        intger_char = {
	        '0':[],
	        '1':[],
	        '2':['a','b','c'],
	        '3': ['d', 'e', 'f'],
	        '4': ['g', 'h', 'i'],
	        '5': ['j', 'k', 'l'],
	        '6': ['m', 'n', 'o'],
	        '7': ['p', 'q', 'r', 's'],
	        '8': ['t', 'u', 'v'],
	        '9': ['w', 'x', 'y', 'z']
	        }

	        if len(digits) == 0:
	            return []
	        else:
	            rlist = intger_char[digits[0]]
	            for num in digits[1:]:
	                temp = []
	                for m in intger_char[num]:
	                    for item in rlist:
	                        temp.append(item + m)
	                rlist = temp
	        return rlist

I once found a pretty good solution, which uses recursion. I copy that code as following:

	class Solution:
	    def letterCombinations(self, digits):
	        """
	        :type digits: str
	        :rtype: List[str]
	        """
	        result = []
	        if len(digits) == 0:
	            return result

	        int_to_char = {'2': ['a', 'b', 'c'],
	                       '3': ['d', 'e', 'f'],
	                       '4': ['g', 'h', 'i'],
	                       '5': ['j', 'k', 'l'],
	                       '6': ['m', 'n', 'o'],
	                       '7': ['p', 'q', 'r', 's'],
	                       '8': ['t', 'u', 'v'],
	                       '9': ['w', 'x', 'y', 'z']}

	        # backtracking function
	        def f(s, idx):
	            if idx == len(digits):
	                result.append(s)
	            else:
	                for char in int_to_char[digits[idx]]:
	                    f(s+char, idx+1)
	        f('', 0)
	        return result

## 18.

.....

## 19. Remove Nth Node From End of List

This question requires knowledge about linked list, because in Python language, we can use list to substitute linked list, thus, we can store numbers into the a list first, then we can delete number in certain postion. In the end, we can get the final linked list:

	class Solution:
	    def removeNthFromEnd(self, head, n):
	        temp = head
	        mlist = []
	        while temp != None:
	            mlist.append(temp.val)
	            temp = temp.next
	        del mlist[len(mlist) - n]	        
	        return mlist

`note: We can make progress on my algorithm question.`

## 20. Valid Parentheses

This is an easy question, the only data structure we should use is stack. We can first append left parenthesises into stack, then we can pop the elements from the stack, if they are compatible, go on, else, return False. Here is the code as following:

	class Solution:
	    def isValid(self, s):
	        mystack = []
	        sdict = {")":"(","]":"[","}":"{"}
	        for item in s:
	            if item in sdict.values():
	                mystack.append(item)
	            elif len(mystack) > 0 and sdict[item] == mystack.pop():
	                continue
	            else:
	                return False
	        return not mystack
