## 338. Counting Bits

The idea here is that when counting in binary the previous number of bits are utilized over and over, and the furthest 0 gets manipulated to a 1. Therefore it is much more efficient to track where you are in the repeating sequence and just add 1. Because binary is to the power of 2 everytime our number doubles we add a 1 to the furthest digit then repeat all previous bits until our number doubles again. This is captured by our OFFSET variable which doubles when it is reached. We then perform wizard math to just return the 1's count of all previous stuff.

    dp = [0] * (n + 1)
    offset = 1

    for i in range(1, n + 1):
        if offset * 2 == i:
            offset = i

        dp[i] = dp[i - offset] + 1

    return dp

## 136. Single Number

Use the XOR operator ^ which compares two numbers' bits and returns the bits 0 if 2 0's, 1 if 0 and 1, or 0 if 2 1's

## 1318. Minimum Flips

---THIS USES BITWISE OR WHICH IS DIFFERENT FROM XOR---
--- 0|0 = 0    1|0 = 1   0|1 = 1  1|1 = 1 ---

Here we use the &1 property to look at the last bit of a,b and c. Then we use the shift operator >>1 to move one bit over and repeat.

Big takeaway is that a & 1 return the last bit of a.

    ans = 0
    while a or b or c:
        t1, t2, t3 = a & 1, b & 1, c & 1
        if (t1 | t2) != t3:
            if t3 == 1:
                ans += 1
            else:
                ans += (t1 + t2)

        a >>= 1
        b >>= 1
        c >>= 1
    return ans
