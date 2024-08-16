## 17. Letter Combinations of a Phone Number

I was on the right track but didn't know how to implement it. I feel like the main point of this problem is the implementation as the answer is very intuitive, just return value for every combo which ends up being 3*3*3*3 combinations for 4 digits(maybe 4*4*4*4 if all 7 or 9).
Answer is to implement a recursive function that adds a letter for every letter.

    numbers = {
        "2": "abc",
        "3": "def",
        "4": "ghi",
        "5": "jkl",
        "6": "mno",
        "7": "pqrs",
        "8": "tuv",
        "9": "wxyz"
        }

    answer = []

    def build(i, string1):
        if len(string1)==len(digits):
            answer.append(string1)
            return
        for character in numbers[digits[i]]:
            build(i+1, string1 + character)

    if digits:
        build(0, "") ## enter blank string initially and starting position of digits
    return answer


## 216. Combination Sum III

For this we create a recursive function that passes through our number, our number list, and our number list sum.
From there we filter out if number list sum is > target and make sure there are no repeating numbers by only adding j in range i to 9 rather than 1 to 9.

    answer = []
    def build(i, combo, total):
        if total == n and len(combo)== k:
            answer.append(combo)
            return
        for j in range(i, 10):
            if total + j > n:
                break
            build(i+1, combo+[i], total+i)

    build(1, [], 0)
    return answer
