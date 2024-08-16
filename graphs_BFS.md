## 1926. Nearest Exit From Entrance

This one was a little squirrely and even the answser I ended up copying only works the way he had it, and doesnt work if you change the directions around and check up,left,right,down in a different order. To me this means that to truely solve this problem we need to track more info but the timeout constraints arent correctly defined. I solved this problem but with way worse computation speed.

def nearestExit(self, maze: List[List[str]], entrance: List[int]) -> int:

    rows = len(maze)
    columns = len(maze[0])

    startx, starty = entrance
    q = collections.deque()
    INF = 10**20

set distance for each spot instead of tracking seen or unseen

    distance = [[INF]*columns for _ in range(rows)]

this function adds the xy to the stack and appends a distance to it

    def enqueue(x,y,d):
        distance[x][y] = d
        q.append((x,y,d))

    enqueue(startx, starty, 0)

    directions = [(1,0), (0,1), (-1,0), (0,-1)]

    while len(q)>0:
        x,y,d = q.popleft()

since we only append open spots, we can check the position to see if its an exit and not the entrance

        if x == 0 or x == rows-1 or y == 0 or y == columns-1:
            if not (x == startx and y == starty):
                return d

This takes the directions tuples and makes a series of nx,ny tuples for each peripheral

        for dx, dy in directions:
            nx, ny = x+dx, y+dy

check if its inside the bounds before checking if its a wall, that way we get no index errors

            if 0 <= nx < rows and 0 <= ny < columns and maze[nx][ny] != "+" and distance[nx][ny] == INF:
                enqueue(nx,ny, d+1)

This line is weird b/c i think we are kinda checking it above, but if we remove this the function performs worse, and if we remove the above then the function fails some testcases

                if nx == 0 or nx == rows or ny == 0 or ny == columns-1:
                    return d+1
    return -1

## 994. Rotting Oranges

def orangesRotting(self, grid: List[List[int]]) -> int:

    # add all rotting oranges to stack
    # time set to infinity for oranges, set time to 0 for rotten or empty spaces
    # bfs from rotting oranges and set time
    # return max time or -1 if infinity

    R = len(grid)
    C = len(grid[0])
    INF = 10**20
    time = [[INF]*C for _ in range(R)]
    q = deque()

    for x in range(R):
        for y in range(C):
            if grid[x][y] == 2:
                q.append((x,y,0))
                time[x][y] = 0
            if grid[x][y] == 0:
                time[x][y] = 0


    def enqueue(x,y,t):
        time[x][y] = t
        q.append((x,y,t))

    directions = [(1,0), (-1,0), (0,1), (0,-1)]

    while q:
        x,y,t = q.popleft()
        for dx, dy in directions:
            nx, ny = x+dx, y+dy

if new x and new y within grid and an orange that hasnt been seen, append

            if 0<= nx < R and 0 <= ny < C and grid[nx][ny] == 1 and time[nx][ny]==INF:
                enqueue(nx,ny,t+1)

weird takeway lesson for how list comprehension works with nested lists

    answer = max(x for inner_list in time for x in inner_list)

    if answer == INF:
        return -1
    return answer
