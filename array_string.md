## Arrays/Strings
1768 - np
## 1071. Greatest Common Divisor of Strings

## Shawnify
    if str1 + str2 != str2 + str1:
        return ""
    variable = gcd(len(str1), len(str2))
    return str1[:variable]
This problem gave me a bit of trouble conceptually. GCD and LCD seems to be a weakness.

    len1, len2 = len(str1), len(str2)

We establish the length of each string because we need to compare the potential GCD string length with these to see if it is even a candidate. ie str1 = 9 and str2 = 6, GCD is 3 so don't check strings of length 2, 4, 5, 6, 7 , 8, 9

    def Divisor(length):
            if len1%length or len2%length:
                return False
            f1, f2 = len1//length, len2//length
            return str1[:length]*f1 == str1 and str1[:length]*f2 == str2

This helper function gets executed later but it is checking if the GCD candidate is a divisor, and checking if the actual GCD string when expanded to the full length of each string creates the same string.

It returns True or False.

    for length in range(min(len1,len2),0,-1):
            if Divisor(length):
                return str1[:length]


This checks potential gcd lengths in range of the smallest string, backwards bc we want GCD not LCD.
If our helper function returns True (correct GCD length and string match) then this returns the actual string of GCD.

    return ""

Otherwise we return an empty string to show there was no GCD found.
 ---
1431 - np

605 - np

345 - np

151 - np

## 238 - Product Of Sum Except Self
range("how far", "where it starts", "what increment") ie range(len(nums)-1, -1, -1) goes for full list, starting from -1, backwards (-1)

I remembered it was a prefix/postfix question to keep it O(n). Hardest part was trying to iterate backwards because I was trying to use the index but not doing it correctly. This solution uses range() and range(len(nums)-1, -1,-1)

    answer = [1]*len(nums)

        prefix = 1

        for i in range(len(nums)):
            answer[i] = answer[i] * prefix
            prefix *= nums[i]

        postfix = 1

        for i in range(len(nums)-1,-1,-1):
            answer[i] = answer[i] * postfix
            postfix *= nums[i]

        return answer

 ---
## 443. String Compression -- struggling with this
The main difficulty of this problem is that they want constant space so we must modify the original list "chars"

    i = 0
i is the index of the original list that we are inserting to

    counter = 1

consecutive number count

    for j in range(1, len(chars) + 1):

create variable j and iterate over it from the 2nd index to the last index of chars

        if j < len(chars) and chars[j] == chars[j-1]:

-not sure why we have to check if j < len chars if we establish that it is in the range

-I think its bc we are modifying the list

            counter += 1
        else:
            chars[i] = chars[j-1]

-i is the index we wish to modify, j-1 is the last consecutive letter of the current streak that just ended

            i = i + 1

-move to the next i to be modified

            if counter > 1:
                for digit in str(counter):
                    chars[i] = digit
                    i += 1
            counter = 1

-if there were consecutive letters, add the counter to the list, but make it a string and loop over each digit bc fuck it we are appending numbers as single digits instead of a fucking number bc we jerk off to javascript at night

    return i

-they want you to return the length of chars at the end, the problem is also looking at chars and comparing it to the expected modifications
