## 933. Number of Recent Calls

Had to look this up because it had a built in function and class which I am not good at.
Explanation makes sense, add each ping to a queue and then pop them from the queue if they are older than 3000ms.
Return count of whats in queue.

    def __init__(self):
        self.q = deque()
        self.count = 0
    def ping(self, t: int) -> int:
        self.q.append(t)
        self.count += 1
        while self.q and self.q[0]<t-3000:
            self.q.popleft()
            self.count -=1
        return self.count
