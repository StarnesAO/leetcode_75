## 841. Keys and Rooms

I think there is a problem with a testcase unless I'm not reading things correclty.

nevermind I understand now I'm an idiot time to go to bed.

** update from the future I am an idiot but not a hopeless case. Solved without lookup on second glance the next week. Not optimal runtime but great on memory.

    stack = [rooms[0]]
    visited = [0]

    while stack:
        keys = stack.pop()
        for key in keys:
            if key not in visited:
                stack.append(rooms[key])
                visited.append(key)

    if len(visited) == len(rooms):
        return True
    return False

## Number of Provinces

Literally the worst running program that passes, but it runs baby!
This is one of the better running programs. I used DFS with a visited list and no recursion.
This solution is more succinct and uses recursion.
- Establish N as number of nodes, visited, and a count
- Create a DFS function that takes in the node and recursively does a DFS on "j" connections to "i"
- Afterwards loop through all i's and if they are not in visited do a DFS and increase the province count

    N = len(isConnected)
    visited = set()
    ans = 0

    def dfs(i : int):
        visited.add(i)

        for j in range(N):
            if isConnected[i][j] and j not in visited:
                dfs(j)

    for i in range(N):
        if i not in visited:
            dfs(i)
            ans += 1

    return ans

## 1466. Reorder Routes to Make all paths lead to city center

I feel like it is similar to something I've done but definitely still confusing.
Mistakes: I was trying to loop through the connections list and pool everything that led to zero together, then count if some node in the lump lead to something outside of it. Almost works but doesn't account for what is a neighbor to city 0 so it inflates the count when it looks at cities that point towards zero but where they point hasn't been assessed in the correct order.




--- Neetcode answer ---

- establish edges
- establish neighbors (so we know correct directions to traverse)
- if neighbor, city NOT IN edges, count (this means that the city points to neighbor and thus AWAY)
- add neighbor to visited and recursively run DFS on neighbor
-

    # start at city 0
    # check neighbors
    # count outgoing edges

    edges = {(a,b) for a, b in connections}
    neighbors = { city: [] for city in range(n) }
    visited = set()
    changes = 0

    # Must establish neighbors so a=>b and b=>a not just a => b
    for a,b in connections:
        neighbors[a].append(b)
        neighbors[b].append(a)

    def DFS(city):
        # pass through city
        nonlocal edges, neighbors, visited, changes
        # check that city's neighbors
        for neighbor in neighbors[city]:
            if neighbor in visited:
                continue
            # if the neighbor doesn't lead to the city, flip it
            if (neighbor, city) not in edges:
                changes +=1
            # add neighbor to visited
            visited.add(neighbor)
            # run DFS on neighbor
            DFS(neighbor)

    # initialize on city 0 and propogate out from there
    visited.add(0)
    DFS(0)
    return changes

## 399. Evaluate Division

Very intersting problem where we are given a list of variable pairs and their resulting division value. With this we need to determine a set of queries that can be based on these variables, reversed, or unrelated variables. My initial thoughs are that we need to treat it like the previous problem and find edges and relations(neighbors).

If a,b = 2 then b,a = .5

So we created a map of a to b and the value, and b to a and the inverse value.

Then we perform BFS on the query using the q0 as source and q1 as taret.

    edges = collections.defaultdict(list) #map a to [b, a/b]
                                          #map b to [a, b/a]
    #equations = [["a","b"],["b","c"]]

    #values = [2.0,3.0]

    for i, equation in enumerate(equations):
        a,b = equation
        edges[a].append([b, values[i]])
        #edges[a].append(b, 2.0)
        edges[b].append([a, 1/values[i]])
        #edges[b].append(a, .5)

    # source = a, target = c
    def bfs(source, target):
        # if there query uses an unseen value, return -1
        if source not in edges or target not in edges:
            return -1
        # BFS house keeping, queue, visited, append start to both
        q, visited = deque(), set()
        q.append([source, 1])
        visited.add(source)
        # while that continues if node is connected and we haven't found target
        while q:
            # node is a,b,c etc
            # weight is the total multiplication from source to this point, i.e. if a=>b is 2 and b=>c is 3, total at c is 6
            node, weight = q.popleft()
            if node == target:
                return weight
            for neighbor, value in edges[node]:
                if neighbor not in visited:
                    q.append([neighbor, weight*value])
                    visited.add(neighbor)
        return -1

    #creates list of values from doing BFS on queries
    return [ bfs(q[0], q[1]) for q in queries]
