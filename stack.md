## 2390. Removing Stars From a String

Solved on my own using a deque and popping.

## 735. Asteroid Collision

ended up looking it up sadly. Loop over the initial list and append to the stack under certain conditions.

    def asteroidCollision(self, asteroids: List[int]) -> List[int]:

        stack = []

        for asteroid in asteroids:

            while stack and stack[-1] > 0 > asteroid:
                ## stack going right asteroid going left
                if abs(stack[-1]) > abs(asteroid):
                    break
                elif abs(stack[-1]) < abs(asteroid):
                    stack.pop()
                else:
                    stack.pop()
                    break

            else:
                stack.append(asteroid)

        return stack

## 394. Decode String

I was on the right track searching for "]" but got a little stuck so looked at the neetcode video. I started coding along/ahead of him but still needed help to finish.

step 1. append to the stack until you get a "]"
step 2. pop from the stack to create the substring
step 3. find out what k is and add the substring to the stack k times
step 4. profit

    def decodeString(self, s: str) -> str:

        stack = []

        for char in s:
            if char != "]":
                stack.append(char)
            else:
                substring = ""
                while stack[-1] != "[":
                    substring = stack.pop() + substring
                stack.pop()
                k = ""
                while stack and stack[-1].isdigit():
                    k = stack.pop() + k
                stack.append(int(k)*substring)
        return "".join(stack)
