## 452. Minimum Number of Arrows to Burst Balloons

sort - nlogn

    points.sort()
    answer = len(points)
    previous = points[0]
    for i in range(1, len(points)):
        current = points[i]
        if current[0] <= previous[1]:
            answer -= 1
            ## here we want to set previous to first of current and min of either current/previous so we only decrement again if a third balloon is in both ranges.
            previous = [current[0], min(current[1], previous[1])]
        else:
            previous = current
    return answer

## 435 Non-Overlapping Intervals

    intervals.sort(key=lambda x: x[1])
    n = 0
    j = intervals[0][1]
    for il in intervals:
        if j > il[0]:
            n += 1
        else:
            j = il[1]
    return n-1
