# 1768. Merge Strings Alternately

## 题目 / Problem

### English

You are given two strings `word1` and `word2`. Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return the merged string.

### 中文

给定两个字符串 `word1` 和 `word2`。

请按照交替顺序合并两个字符串，并且从 `word1` 开始添加字符。

如果其中一个字符串比另一个更长，则将多出来的字符直接追加到合并后字符串的末尾。

返回合并后的字符串。

---

## 示例 / Examples

### Example 1

**Input:**

```python
word1 = "abc"
word2 = "pqr"
```

**Output:**

```python
"apbqcr"
```

**Explanation:**

```text
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
```

**中文解释：**

两个字符串长度相同，所以按顺序交替合并：

```text
a -> p -> b -> q -> c -> r
```

最终得到：

```python
"apbqcr"
```

---

### Example 2

**Input:**

```python
word1 = "ab"
word2 = "pqrs"
```

**Output:**

```python
"apbqrs"
```

**Explanation:**

```text
word1:  a   b
word2:    p   q   r   s
merged: a p b q   r   s
```

**中文解释：**

先交替合并 `"a"`、`"p"`、`"b"`、`"q"`。

因为 `word2` 更长，所以把剩下的 `"rs"` 直接追加到最后。

最终得到：

```python
"apbqrs"
```

---

### Example 3

**Input:**

```python
word1 = "abcd"
word2 = "pq"
```

**Output:**

```python
"apbqcd"
```

**Explanation:**

```text
word1:  a   b   c   d
word2:    p   q
merged: a p b q c   d
```

**中文解释：**

先交替合并 `"a"`、`"p"`、`"b"`、`"q"`。

因为 `word1` 更长，所以把剩下的 `"cd"` 直接追加到最后。

最终得到：

```python
"apbqcd"
```

---

## 限制条件 / Constraints

```text
1 <= word1.length, word2.length <= 100
word1 and word2 consist of lowercase English letters.
```

中文：

```text
1 <= word1 的长度, word2 的长度 <= 100
word1 和 word2 只包含小写英文字母
```

---

## 思路 / Approach

这题是一个基础字符串模拟题。

题目要求我们从 `word1` 开始，交替取两个字符串的字符。

也就是：

```text
先取 word1[0]
再取 word2[0]
再取 word1[1]
再取 word2[1]
...
```

但是两个字符串长度可能不一样。

所以不能直接同时取 `word1[i]` 和 `word2[i]`，否则较短的字符串会越界。

解决方法是：

1. 先创建一个空列表 `result`，用来存放最终结果的每个字符。
2. 找到两个字符串中较长的长度 `max_length`。
3. 用 `for` 循环从 `0` 遍历到 `max_length - 1`。
4. 每一轮先判断 `word1` 是否还有第 `i` 个字符。
5. 如果有，就把 `word1[i]` 加入 `result`。
6. 再判断 `word2` 是否还有第 `i` 个字符。
7. 如果有，就把 `word2[i]` 加入 `result`。
8. 最后用 `"".join(result)` 把列表拼成字符串。

---

## 代码 / Code

```python
class Solution(object):
    def mergeAlternately(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: str
        """
        
        result = []
        max_length = max(len(word1), len(word2))

        for i in range(max_length):
            if i < len(word1):
                result.append(word1[i])

            if i < len(word2):
                result.append(word2[i])
        
        return "".join(result)
```

---

## 代码解释 / Code Explanation

### 1. 创建结果列表

```python
result = []
```

这里的 `result` 用来存放合并后的每一个字符。

比如最后可能会变成：

```python
["a", "p", "b", "q", "c", "r"]
```

---

### 2. 找到更长的字符串长度

```python
max_length = max(len(word1), len(word2))
```

因为两个字符串长度可能不一样，所以循环次数应该按照更长的那个字符串来。

比如：

```python
word1 = "ab"
word2 = "pqrs"
```

那么：

```python
len(word1) = 2
len(word2) = 4
max_length = 4
```

这样才能把 `word2` 剩下的 `"rs"` 也加进去。

---

### 3. 遍历每一个位置

```python
for i in range(max_length):
```

这里的 `i` 表示当前处理的位置。

比如：

```text
i = 0
i = 1
i = 2
i = 3
```

---

### 4. 如果 `word1` 还有字符，就加入结果

```python
if i < len(word1):
    result.append(word1[i])
```

这句是在判断：

```text
word1 里面还有没有第 i 个字符？
```

如果有，就把它加入 `result`。

---

### 5. 如果 `word2` 还有字符，也加入结果

```python
if i < len(word2):
    result.append(word2[i])
```

这句是在判断：

```text
word2 里面还有没有第 i 个字符？
```

如果有，就把它加入 `result`。

---

### 6. 把列表拼成字符串

```python
return "".join(result)
```

`join` 的作用是把列表里的字符串拼接起来。

比如：

```python
result = ["a", "p", "b", "q", "c", "r"]
```

执行：

```python
"".join(result)
```

结果就是：

```python
"apbqcr"
```

这里的 `""` 表示中间不加任何东西，直接无缝拼接。

---

## 运行过程 / Walkthrough

以 Example 2 为例：

```python
word1 = "ab"
word2 = "pqrs"
```

初始：

```python
result = []
max_length = 4
```

循环过程：

```text
i = 0
word1[0] = "a"，加入 result
word2[0] = "p"，加入 result
result = ["a", "p"]

i = 1
word1[1] = "b"，加入 result
word2[1] = "q"，加入 result
result = ["a", "p", "b", "q"]

i = 2
word1 已经没有第 2 个字符，不加入
word2[2] = "r"，加入 result
result = ["a", "p", "b", "q", "r"]

i = 3
word1 已经没有第 3 个字符，不加入
word2[3] = "s"，加入 result
result = ["a", "p", "b", "q", "r", "s"]
```

最后：

```python
"".join(result)
```

得到：

```python
"apbqrs"
```

---

## 复盘 / Review

这题的核心套路是：

```text
用一个 index 同时遍历两个字符串
每次先判断有没有越界
没有越界就加入答案
```

以后看到这种题目关键词：

```text
merge
alternating order
append remaining characters
```

可以先想到：

```text
用循环模拟整个合并过程
```

这题不用想复杂，本质就是按照题目要求一步一步把字符放进结果里。
````
