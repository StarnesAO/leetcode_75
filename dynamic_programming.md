## 1137. Tribonacci

come back to this bc I kinda looked it up but also was in a zoom call while looking at it initially

## 746. Min Cost Climbing Stairs

Also kinda looked this one up. I had an epiphany while watching the neetcode explanation then solved it without looking at his code. The realization that you need to iterate over the list in reverse to get the total cost to get to the end from that point helped.

## 198. House Robber

Heralded as the crux of dynamic programming the key it seems to dynamic programming is to dynamically update the values of your list correctly and return the max of your options at the end.

    r1, r2 = 0,0
    #[r1, r2, n, n+1...]
    for n in nums:
        temp = max(n+ r1, r2)
        r1 = r2
        r2 = temp
    return r2


## 790. Domino and Tromino Tiling

This problem was worded like absolute hot garbage. After watching a video on this problem I realized what they meant. The problem is a simple number sequence where y[n] = y[n-1]*2 + y[n-3] so they are just asking you to initialize the first 4 numbers of the pattern and then apply this formulat to find all the numbers dynamically up to n. It's like solving for a tribonacci number but with a weird broken english domino based story.


    mod = 1e9 + 7
    dp = [0,1,2,5] + [0]*(n-3)
    for i in range(4,n+1):
        print(i)
        dp[i] = 2*dp[i-1] + dp[i-3]
        dp[i] %= mod
    return int(dp[n])


## 62. Unique Paths

[15][10][6] [3] [1]
[5] [4] [3] [2] [1]
[1] [1] [1] [1] [1]


    def uniquePaths(self, m: int, n: int) -> int:
        row = [1]*n
        for i in range(m-1):
            new_row = [1]*n
            for j in range(n-2, -1, -1):

each spot is equal to the right value and down value sum

                new_row[j] = new_row[j+1]+row[j]
            row = new_row
        return row[0]

## 72. Edit Distance
  W     O   R   D
W []   []  []  [] [4]
O []   []  []  [] [3]
R []   []  []  [] [2]
D []   []  []  [] [1]
  [4] [3] [2] [1] [0]

The idea is to make a grid that holds the minimum edits required to get from everything after that letter to everything after the other letter, aka if W and R, then WORD and RD.

So we start at "" and "" with 0.
Then up and left will be "" and D, which takes 1 edit.
Left or up will be "" and R, which takes 2 edits. Etc..
** We then look at the last letter of each word, and if they are the same we set the value to min from right, down, and diag.
** If they are different we do min of Righ, down, and diag but add 1
** Continue this all the way to the first letters, this is our answer.

    def minDistance(self, word1: str, word2: str) -> int:
        R = len(word2)+1
        C = len(word1)+1
        cache = [[float("inf")]*R for i in range(C)]

        for j in range(R):
            cache[C-1][j] = R -1 - j
        for i in range(C):
            cache[i][R-1] = C - 1 - i

        for i in range(C - 2, -1, -1):
            for j in range(R - 2, -1, -1):
                if word1[i] == word2[j]:
                    cache[i][j] = cache[i+1][j+1]
                else:
                    cache[i][j] = 1 + min(cache[i][j+1], cache[i+1][j+1], cache[i+1][j])

        return cache[0][0]


## 1143. Longest Common Subsequence

More neetcode. Similar to the above problem with the grid approach. Ghost row/column is 0's. If letters are the same take diagonal + 1, otherwise do max of right or down.

    def longestCommonSubsequence(self, text1: str, text2: str) -> int:

        R = len(text1)
        C = len(text2)

        grid = [[0 for j in range(C+1)] for i in range(R+1)]

        for i in range(R -1, -1, -1):
            for j in range(C -1, -1, -1):
                if text1[i] == text2[j]:
                    grid[i][j] = 1 + grid[i+1][j+1]
                else:
                    grid[i][j] = max(grid[i+1][j], grid[i][j+1])

        return grid[0][0]


## 714. Best Time to Buy and Sell Stock

Pretty straight forward once you see the answer. Still Tricky. I was correct that it was very similar to the rober problem. Misread the problem and thought the fee was subtracted for buying and selling not just selling.

    def maxProfit(self, prices: List[int], fee: int) -> int:

        buy = 0
        sell = 0
        buy = -prices[0]

        for x in prices[1:]:
            buy2 = max(buy, sell - x)
            sell2 = max(sell, buy + x - fee)
            buy = buy2
            sell = sell2

        return sell
