## 199. Binary Tree Right Side View

set up just like other searches, tracked depth and appended right first, w/ FIFO popleft()

## 1161. Maximum Level Sum of a Binary Tree

Set up mostly the same, tracked depth and created a dictionary of depths that held the sums as values.
Slight nuisance geting key associated with max value in dict, aka max(dict, key = dict.get)

