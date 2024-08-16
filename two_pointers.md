## Two Pointers

11. Container With Most Water

My initial naive approach was to take i=0 and j =1, and increment j looking for a max, then increase i by 1 and do it all again. This passed initial tests but I had 2 while loops and it timed out on the real tests.

The more correct solution takes pointers i = 0 and j = length of container, and places them in a while loop that calculates current water height, and increments or decrements the lower of the heights. So if height[i] > height[j] we would move j and if height[j] > height[i] we move i.

    i = 0
        j = len(height)-1
        water = 0
        while i<j:

            current = min(height[i], height[j]) * (j-i)
            if water < current:
                water = current
            if height[i] < height[j]:
                i+=1
            else:
                j-=1


        return water

1679. Max Number of K-Sum Pairs

A crucial aspect of "two pointers" questions that I am noticing is that you must arrange the list into a meaningful order so the pointers gain max efficiency, otherwise you are stuck with a while loop per pointer, and n^2 for 2 pointers.

The pattern for two pointers is to arrange the list, then establish a left pointer at index 0 and a right pointer at the end of the list, then converge the pointers while counting for the test case answer.

    nums.sort()

        l,r,count = 0, len(nums)-1, 0

        while l<r:
            s = nums[l] + nums[r]
            if s ==k:
                count +=1
                l += 1
                r -= 1
            elif s < k:
                l+=1
            else:
                r -=1

        return count

The k sum pairs question, once the list is sorted, just compares the current sum to k and moves the right pointer if the sum is > k and the left pointer if sum < k

## Timsort

So python's sort() function uses a Tim sort named after tim peters. it is STABLE meaning it leaves similar values in order.

(5,3,3,3,1) --> (1,3,3,3,5) and 3's wont get shuffled

it is a combo of merge and insertion with O(nlogn) worst case or O(n) if sorted
