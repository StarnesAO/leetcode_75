## Sliding Window

The idea with sliding window problems is that it is more efficient to make a large calculation once, then subsequently make small calculations while traversing the list.

643. Maximum Average Subarray

    largest_sum = sum(nums[0:k])
        print(largest_sum, k)
        current_sum = largest_sum

        new_sum = 0
        i=1

        if len(nums) == 1:
            return nums[0]

        while i <= len(nums)-k:

            current_sum = current_sum - nums[i-1] + nums[i+k-1]

            if current_sum > largest_sum:
                largest_sum = current_sum

            i+=1

        return (largest_sum/k)

## 1004. Max Consecutive Ones III

    i = 0

    for j in range(len(nums)):

k is subtracting 1 - value of nums[j] so when nums[j] is another zero, k goes down by one, and when nums[j] is a 1 k stays the same.

        k -= 1 - nums[j]

if k is less than 0 we have more zeros in the window than we have flips so move our starting index, and if it is a zero, k goes up

use "if" not "while" because we don't want the window to shrink

        if k < 0:
            k += 1 - nums[i]
            i += 1

    return j - i + 1

## 1493. Longest Subarray of 1's After Deleting One.

Was able to solve this by deconstructing the method used above and repurposing.
Essentially the same but k = 1
Extremely useful blueprint if you understand it. (do i?)
