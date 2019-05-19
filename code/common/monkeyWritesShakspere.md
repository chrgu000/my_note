```python
import random
import gc


def generateOne(strlen):
    alphabet = 'abcdefghijklmnopqrstuvwxyz '
    res = ''
    for i in range(strlen):
        res = res + alphabet[random.randrange(27)]
    return res


def score(goal, testStr):
    score = 0
    for i in range(len(goal)):
        if goal[i] == testStr[i]:
            score = score + 1
    return score / len(goal)


def main():
    goalStr = 'methinks it is like a weasel'
    newStr = generateOne(28)
    best = 0
    newScore = score(goalStr, newStr)
    times = 0
    while newScore < 1:
        if newScore > best:
            print(newScore, newStr, times)
            best = newScore
            gc.collect()
        newStr = generateOne(28)
        newScore = score(goalStr, newStr)
        times += 1


main()
```