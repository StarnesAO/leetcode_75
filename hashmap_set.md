## 2215. Find the Difference of Two Arrays

Solved by myself, key takeaway is that a set can not be manipulated so you must convert it into a list.

## 1207. Unique Number of Occurences

Pretty sure I self solved, we have done this type problem in class a few times.

## 1657. Determine if Two Strings are Close

Solved on my own with no time constraints.

Very reminiscent of molecular translations in my mind. Use set() to compare letters and use a dictionary of counts to determine if numbers can be swapped.

    set1 = [x for x in set(word1)]
    set2 = [x for x in set(word2)]
    dict1 = {}
    dict2 = {}
    count1 = []
    count2 = []
    for word in word1:
        if word not in dict1:
            dict1[word]=1
        else:
            dict1[word]+=1
    for word in word2:
        if word not in dict2:
            dict2[word]=1
        else:
            dict2[word]+=1

    for value in dict1.values():
        count1.append(value)
    for value in dict2.values():
        count2.append(value)

    count1.sort()
    count2.sort()
    set1.sort()
    set2.sort()

    return (count1 == count2 and set1 == set2)

After looking at answer this is ugly. You can just one line it by doing set1() == set2() and sorted Counter functions. Counter(word1) == dict of letter counts.

Key takeaways -- Counter() function and don't sort sets.

## 2352. Equal Row and Column Pairs

Solved but not with a hash map or set so definitely not intended. Just brute force made a new list that contains columns.

Most online solutions look similar but they are using collections.counter(tuple(row) for row in grid) to python optimize the counting. Not sure exactly what this does.
