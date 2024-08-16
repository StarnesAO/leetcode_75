## Monotonic Stacks

739. Daily Temperatures

Similar to the maze but here we are storing a list (this is what stumped me) that contains the value and the index.

    answer = [0]*len(temperatures)
    stack = []

    for index, temp in enumerate(temperatures):

        while stack and temp > stack[-1][0]:

            position = stack.pop()

            answer[position[1]] = index-position[1]

        stack.append([temp,index])

    return answer


901. Online Stock Span

The presentation of this was very weird to me. I had a hard time navigating the function aspects of calling self.stack and conceptually why/what the span was. I think it was because it was a concept but also being stored as a variable on the stack.

    class StockSpanner:

    def __init__(self):
        self.stack = []

    def next(self, price: int) -> int:

        previous_days_since_higher = 1

        while self.stack and price >= self.stack[-1][0]:

            previous_days_since_higher += self.previous_days_since_higher[-1][1]

            self.stack.pop()

        self.stack.append([price,previous_days_since_higher])

        print(self.stack)

        return self.stack[-1][1] ## span

The span is a count of how many days since the price was higher. The stack contains a list of [price, span]. We save the span not because we are returning it later, we already return the span when the price is inputted by calling next, but because we need a tally of how many previous days that stored price "ate" from the stack. When the next function is called, the given price is compared with the smallest(topmost) price on the stack. If it is larger it "eats" the price (pops it) and continues through the stack, eating and adding span values to it's own until it gets to a larger price. Once it gets to the larger price it satisfies the definition of a span (consecutive days at a lower price) and adds todays price and accumulated span to the stack, and returns the span number.
