## Binary Search Basics
l,r=0,n
middle = l+r//2
Basic idea is to have a left,right = min,max and then adjust the middle on a sorted list until everthing above or below doesnt fit criteria then return the necessary bits.



## 374. Guess Number High or Low

Solved by myself  with no time contraints. I used floor division but this leads to infinite loops. Better to use int(n/2) + 1 to avoid this.

    class Solution:
    def guessNumber(self, n: int) -> int:
        high = n
        low = 0
        number = n//2
        answer = guess(number)

        while answer != 0:
            if answer == -1:
                high = number
                if high-low >1:
                    number = (high+low)//2
                    answer = guess(number)
                else:
                    answer = guess(number-1)
                    number -= 1
            if answer == 1:
                low = number
                if high - low >1:
                    number = (high+low)//2
                    answer = guess(number)
                else:
                    answer = guess(number+1)
                    number+=1
        return number


## 2300. Successful Pairs of Spells and Potions

Solved non-optimizing test cases.
Didn't properly implement the core of binary search which is l,r = 0,n with an adjusting midpoint bisection.

     potions.sort()
        res = []
        for i in range(0, len(spells)):
            x = ceil(success/spells[i])
            j = bisect.bisect_left(potions,x)
            res.append(len(potions) - j)

        return res

This answer uses both the ceil function and the bisect function to achieve the binary search in a more efficient way.

ceil(success/spells[i]) returns the min number our potion can be so that potion*spell[i] > success

bisect.bisect_left(potions,x) returns the value of the index at which potions first is greater than x.
if potions = [1,2,3,4,5] and x = 2, bisect_left returns 1, bc at index 1 potions = 2

## 162. Find Peak Element

Seems like most people agree it's weird to use binary search on this question. My first instinct was essentially sliding window and it worked just fine.

    def findPeakElement(self, nums: List[int]) -> int:
        nums = [float(-inf)] + nums + [float(-inf)]
        for i in range(1, len(nums)-1):
            if nums[i-1]<nums[i] and nums[i]>nums[i+1]:
                return i-1

## 875. Koko Eating Bananas

So I sorted the initial list but really didn't need to. This problem seems weird at first but follows the l,r = 0,n formula but n is the max value in the piles list.

The actual binary search is on the possible values of k (eating speed). Create a binary search that compares time spent to eat all the banana piles at time k to the max allowed time h.

**Make sure to realize that if time spent at k is equal to h, lower k to see if it results in the same time but at a lower eating speed.

    l,r = 1,max(piles)
        answer = r
        while l<=r:
            time = 0
            k = (l+r)//2
            for pile in piles:
                time += math.ceil(pile/k)
            if time > h:
                l=k +1
            elif time <= h:
                answer = min(answer, k)
                r = k -1
        return answer
