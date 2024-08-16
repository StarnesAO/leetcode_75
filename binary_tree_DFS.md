## 104. Maximum Depth of Binary Tree

tripped me up because I was just thinking of using a solution dictionary but knew it was more than I needed. A simple depth counter sufficed so that the stack was the root and its depth.

    if not root:
        return 0
    stack = [[root,1]]
    max_depth = 1
    while stack:
        node, depth = stack.pop()
        if node:
            res = max(res, depth)
            stack.append([node.left, depth+1])
            stack.append([node.right, depth+1])
    return max_depth


## 872. Leaf-Similar Trees

Completed with not much fuss after referencing the above solution.

## 1448 Count Good Nodes in Binary Tree

Completed with not much fuss after referencing the above solution

## 437. Path Sum III

WTF...

no idea what's going on and when I try to translate working code into my own structure for tree traversal it doesn't work. Might have something to do with me not using sub functions to keep a dictionary local?

gist of the answer is that we have a dict of previous sums and if our current sum or (((actually I don't understand what summ - targetSum has to do with this but I'm fried right now)))

    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        self.count = 0
        summ = 0

using defaultdict(int) is different than just using {} it allows you add the value to the dictionary easily with += 1

        sumMap = defaultdict(int)

all working answers use recursive functions - I believe it keeps the summs local

        def traverseTree(curr, summ):
            if not curr:
                return

            summ += curr.val

            if summ == targetSum :
                self.count += 1

            if sumMap.get(summ - targetSum):
                self.count += sumMap[summ - targetSum]

here is why we use defaultdict(int)

            sumMap[summ] += 1

            traverseTree(curr.left, summ)
            traverseTree(curr.right, summ)


            if sumMap.get(summ):
                sumMap[summ] -= 1


        traverseTree(root, 0)
        return self.count


## 1372. Longest ZigZag Path

Homebrewed ugly but it worked, kinda had to look stuff up but it just verified that I was on the right track and had a 1 or a 0 where it shouldn't be.

    stack = [[root, 0, 0]]
    longest = 0
    ## Right = 1, Left = -1
    if not root.left:
        if not root.right:
            return 0
    while stack:
        node, streak, zigzag = stack.pop()

        if not node:
            return

        if streak > longest:
            longest = streak

        if node.left:
            if zigzag == 1:
                stack.append([node.left, streak + 1, -1])
            else:
                stack.append([node.left, 0, -1])
        if node.right:
            if zigzag == -1:
                stack.append([node.right, streak + 1, 1])
            else:
                stack.append([node.right, 0, 1])

    return longest + 1


## 236. Lowest Common Ancestor

We have a binary tree, not a binary search tree.
We wish to return LCA so check if the node is p or q. If it is not then search the left node and the right node.
If we find p or q in the l or r then l/r is set to p or q respectively, if neither is in the l or r then it returns None.
If there is a value in both l and r, then current is the LCA otherwise the returned value from l or r is the LCA.

    if not root:
        return None
    if root == p or root == q:
        return root
    l = self.lowestCommonAncestor(root.left, p, q)
    r = self.lowestCommonAncestor(root.right, p, q)

    if l and r:
        return root
    else:
        return l or r
