# Decode-Ways
A message containing letters from A-Z is being encoded to numbers using the following mapping:   'A' -> 1'B' -> 2...'Z' -> 26   Given a non-empty string containing only digits, determine the total number of ways to decode it. 
Example 1: 

Input: "12"Output: 2Explanation: It could be decoded as "AB" (1 2) or "L" (12). 

Example 2: 

Input: "226"Output: 3Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6). 

Solution: 

This approach for solving the problem is pretty simple and checks all the possible states of each number in the given string.  

Let’s look at the string “226”, which is the example №2. As we know, numbers in the interval [1,26] (including the limits) can either be a single number or be group of two digits. Let’s see how can we group the digits in the example №2. It could be grouped as: 

1) 2 –26 

2) 22- 6 

3) 2 –2 – 6 

Please pay attention that the limits digits only can be grouped with the following digit for the start limit and with the previous digit for the end limit, while all the digits between the limits can be grouped with the following and the previous digits both.  

Ok, now we will look at one more example “1221”, there are 4 digits in the string. How can we group it now? Let's start from the beginning of the string and group each digit with the following one. 

1) 1 – 2 – 2 – 1 

2) 12 – 2 – 1 

3) 12 – 21 

4) 1 – 22 – 1 

5) 1 – 2 – 21 

There are 5 possible ways to decode the line of 4 digits and 3 ways for the line of 3 digits. It looks like the Fibonacci number. And it is! If we try it for the string of 5 digits, it will turn out that there are 8 ways to group the digits. The Fibonacci Sequence is the series of numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ... where the next number is found by adding up the two numbers before it. First two numbers are always 0 and 1, but then it is the sum of 0 and 1 which is 1, the sum of 1 and 1 gives us 2.... So for the number 3 it will be (3-1)+(3-2)=2+1=3. And for the number 4 it will be (4-1)+(4-2)=3+2=5.  

Think of it as the maneuvering field for grouping the digits in the line, where all the digits can either be grouped or stay a single digit in this field, but it always >=1 and<=26. If in the second example “226” we add any digit after the limit 6, then it could not be the Fibonacci Sequence any more, because the number starting from 6 is bigger than 26. And it could not be grouped with the previous number. 

Like 2261, grouping the last two numbers  we will get 61 which is definitely bigger the 26.  

What are those numbers, which break the Fibonacci Sequence?  

They are first of all 10 and 20, because the digit 0 can only be the second digit in the group, but never can be the first one. And in our range from 1 to 26 only two numbers have “0” as the second digit- they are 10 and 20. In this case any other digit in front of “0” will indicate that the example is wrong and there are no ways to decode the string.  

As we have already found out earlier, if the current and following digits form the number, which is bigger than 26, than the second (following) digit can’t be included in the Fibonacci Sequence. It means, that the S[I+1] digit either starts a new sequence or is a single stable number. It surely depends on the next number after the following one.  

Now let’s try to find out how many ways there are to decode this string “12345610121”. 

Check the digits one by one, if the current and following digits form the number, which is >=1 and <=26, excluding numbers 10 and 20.  As we can see, there is the Fibonacci Sequence “123”, than there are 4 stable digits “4,5,6,10”, because 34, 45, 56 are bigger than 26, and the digit “0” only can follow the another digit, but can’t start the number. And then again there are 3 digits that form the Fibonacci Sequence “121”.   

The Fibonacci number for 3 is 3, it means that there are 3 ways to decode the first sequence and also 3 ways to decode the second sequence, lets’ try all the possible ways. 

1) 1 – 2 – 3 – 4 – 5 – 6 – 10 – 1 – 2 – 1 

2) 1 2 – 3 – 4 – 5 – 6 – 10 – 1 – 2 – 1 

3) 1 – 2 3 – 4 – 5 – 6 – 10 – 1 – 2 – 1 

4) 1 – 2 – 3 – 4 – 5 – 6 – 10 – 12 – 1 

5) 1 – 2 – 3 – 4 – 5 – 6 – 10 – 1 – 21 

6) 12 – 3 – 4 – 5 – 6 – 10 – 12 – 1 

7) 12 – 3 – 4 – 5 – 6 – 10 – 1 – 21 

8) 1 – 23 – 4 – 5 – 6 – 10 – 12 – 1 

9) 1 – 23 – 4 – 5 – 6 – 10 – 1 – 21 

Stable numbers are the same in any variation of the decoding, that’s why they don’t affect the result, but they are still important to check if the string is correct. We will check this condition in the beginning of the code along with another one condition. if (s[0] == '0'), the string is incorrect, because number can’t start with “0”. Also if ((s.length() == 1) && (s != "0")), the string consists of only one number and if it is not “0”, then there are only one way to decode the it. 

In the case if both of those conditions are false, we can start checking all the numbers in the string. As we understood from the foresaid, each number we should check for 4 possible conditions: 

1) if it is “0” and it has “1” or “2” in front of it 

2) if the current and the following digits form the number in the correct range from 1 to 26, excluding 10 and 20 

3) in the case that the following number is “0”, we check if the current number is again “1” or “2”, so they can form the excluded 10 and 20 

4) and finally, we check if the current and the following digits form the number that is bigger than 26 

Don’t forget that the loop should finish its work on one digit before the end of the string, because we are checking the current and the following digits together. So, we also need to check if the last one digit isn’t “0” and does it belong to the Fibonacci Sequence or it is a single stable number. 

In fine, let’s find the total number of ways to decode the given string.  For this we need to multiply all the Fibonacci numbers and return the result.  

This approach requires runtime: 4 ms, memory usage: 8.6 MB. 

Its’ space complexity is O(n2) for computing the Fibonacci number and O(n) for checking each number in the string. By changing the way of computing the Fibonacci number, it can be improved to O(n). 

 

 

 
