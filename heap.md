### 215. Kth Largest Element in an Array
use min heap to restrict the heap size to just k elements

    heap = []
    for num in nums:
        if len(heap) < k: ## establishes a heap of size k so that the min is the kth largest element
            heapq.heappush(heap,num)
        else:
            if num > heap[0]: ## if num is larger than min heap, add it, it is the new kth largest so far
                heapq.heappop(heap) ## pops the top of the heap
                heapq.heappush(heap,num) ## adds new larger number to the heap
    return heap[0]

#Time complexity: N * log K ---> N is how many elements get appended to heap after initial k,  K is size of heap, heap   works in log K

#Space complexity: O(K)

#Comparison: Quicksort: O(N^2) worst case
                        # O(1) space

## 2542. Max Subsequence Score

initialize a list of pairs to maintain indexed relations but allow us to sort based on n2

    pairs = [(n1, n2) for n1, n2 in zip(nums1, nums2)]

sort pairs based on a lambda function with parameters(p) set to p[1]

    pairs = sorted(pairs, key = lambda p: p[1], reverse = True)

    min_heap = []
    n1_sum = 0
    answer = 0

    for n1, n2 in pairs:
        n1_sum += n1
        heapq.heappush(min_heap, n1)

        if len(min_heap) > k:
            n1_pop = heapq.heappop(min_heap)
            n1_sum -= n1_pop

        if len(min_heap) == k:
            answer = max(answer, n1_sum*n2)

    return answer

## 2462. Total Cost of Hiring K Workers

Initialize variables

    n = len(costs)
    net_cost = 0

Left, Right are set to indexes associated with number of candidates to be considered. If candidates = 4 then we will look at indexes 0-3, and backwards from -1 to -5

    left = candidates
    right = len(costs) - candidates-1

Establish heaps

    left_heap = costs[:candidates]
    right_heap = costs[max(candidates, len(costs) - candidates):]

    heapify(left_heap)
    heapify(right_heap)


Number of hiring sessions k

    for i in range(k):

If the first candidate from left heap has the minimum cost:
Something to do with two pointers but kind of confusing
Looks like we are pushing to the heap before moving the pointers, whatever

        if not right_heap or (left_heap and right_heap[0]>=left_heap[0]):
            net_cost += heappop(left_heap)
            if left<=right:
                heappush(left_heap, costs[left])
                left+=1
        else:
            net_cost += heappop(right_heap)
            if left<=right:
                heappush(right_heap, costs[right])
                right-=1

    return net_cost

##
