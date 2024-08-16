## Prefix Sum

724. Find Pivot Index

Rightfully so this is an easy question. I iterated over the entire list for each step like a simpleton and it still passed somehow at 5000+ ms runtime. While coding the naive approach I realized it would be more efficient to do a "sliding window" type approach like below but decided to see out the naive approach first.

    right_sum = sum(nums)
    left_sum = 0

    for i, num in enumerate(nums):

        right_sum -= num

        if left_sum == right_sum:

            return i

        left_sum += num

    return -1
