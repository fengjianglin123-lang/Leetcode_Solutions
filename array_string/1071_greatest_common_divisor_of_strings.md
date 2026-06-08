# 1071. Greatest Common Divisor of Strings

## 题目 / Problem

### English

For two strings `s` and `t`, we say "`t` divides `s`" if and only if `s = t + t + t + ... + t`, meaning `t` is concatenated with itself one or more times.

Given two strings `str1` and `str2`, return the largest string `x` such that `x` divides both `str1` and `str2`.

### 中文

对于两个字符串 `s` 和 `t`，如果 `s` 可以由若干个 `t` 拼接而成，那么我们就说 `t` 可以整除 `s`。

也就是说：

```text
s = t + t + t + ... + t
```

给定两个字符串 `str1` 和 `str2`，返回一个最长的字符串 `x`，使得 `x` 同时可以整除 `str1` 和 `str2`。

如果不存在这样的字符串，则返回空字符串 `""`。

---

## 示例 / Examples

### Example 1

**Input:**

```python
str1 = "ABCABC"
str2 = "ABC"
```

**Output:**

```python
"ABC"
```

**Explanation:**

```text
str1 = "ABC" + "ABC"
str2 = "ABC"
```

**中文解释：**

`"ABC"` 可以重复组成 `str1`：

```text
"ABCABC" = "ABC" + "ABC"
```

`"ABC"` 也可以组成 `str2`：

```text
"ABC" = "ABC"
```

所以最长的公共整除字符串是：

```python
"ABC"
```

---

### Example 2

**Input:**

```python
str1 = "ABABAB"
str2 = "ABAB"
```

**Output:**

```python
"AB"
```

**Explanation:**

```text
str1 = "AB" + "AB" + "AB"
str2 = "AB" + "AB"
```

**中文解释：**

`"AB"` 可以重复组成 `str1`：

```text
"ABABAB" = "AB" + "AB" + "AB"
```

`"AB"` 也可以重复组成 `str2`：

```text
"ABAB" = "AB" + "AB"
```

所以最长的公共整除字符串是：

```python
"AB"
```

---

### Example 3

**Input:**

```python
str1 = "LEET"
str2 = "CODE"
```

**Output:**

```python
""
```

**中文解释：**

`"LEET"` 和 `"CODE"` 没有共同的重复基础字符串。

所以返回空字符串：

```python
""
```

---

## 限制条件 / Constraints

```text
1 <= str1.length, str2.length <= 1000
str1 and str2 consist of English uppercase letters.
```

中文：

```text
1 <= str1 的长度, str2 的长度 <= 1000
str1 和 str2 只包含大写英文字母
```

---

## 思路 / Approach

这题的核心是：

如果两个字符串可以由同一个基础字符串重复组成，那么它们拼接的顺序应该不影响最终结果。

也就是说，如果存在一个字符串 `x`，可以同时组成 `str1` 和 `str2`，那么：

```python
str1 + str2
```

应该等于：

```python
str2 + str1
```

比如：

```python
str1 = "ABCABC"
str2 = "ABC"
```

那么：

```python
str1 + str2 = "ABCABCABC"
str2 + str1 = "ABCABCABC"
```

两个结果一样，说明它们有共同的重复结构。

但是如果：

```python
str1 = "LEET"
str2 = "CODE"
```

那么：

```python
str1 + str2 = "LEETCODE"
str2 + str1 = "CODELEET"
```

两个结果不一样，说明它们没有共同的重复结构，直接返回空字符串。

---

如果两个字符串确实有共同的重复结构，那么答案的长度应该是：

```text
str1 长度 和 str2 长度 的最大公约数
```

比如：

```python
str1 = "ABABAB"   # 长度是 6
str2 = "ABAB"     # 长度是 4
```

`6` 和 `4` 的最大公约数是 `2`。

所以答案长度应该是 `2`。

从 `str1` 里面取前 `2` 个字符：

```python
str1[:2]
```

得到：

```python
"AB"
```

所以答案是：

```python
"AB"
```

---

解决方法是：

1. 先判断 `str1 + str2` 是否等于 `str2 + str1`。
2. 如果不相等，说明没有公共重复结构，返回空字符串。
3. 如果相等，说明存在公共重复结构。
4. 计算 `len(str1)` 和 `len(str2)` 的最大公约数。
5. 从 `str1` 里取前 `最大公约数长度` 个字符作为答案。

---

## 代码 / Code

```python
class Solution(object):
    def gcdOfStrings(self, str1, str2):
        """
        :type str1: str
        :type str2: str
        :rtype: str
        """

        if str1 + str2 != str2 + str1:
            return ""

        a = len(str1)
        b = len(str2)

        while b != 0:
            old_a = a
            old_b = b

            a = old_b
            b = old_a % old_b

        gcd_length = a

        return str1[:gcd_length]
```

---

## 代码解释 / Code Explanation

### 1. 判断两个字符串是否有共同重复结构

```python
if str1 + str2 != str2 + str1:
    return ""
```

这一步是在判断 `str1` 和 `str2` 能不能由同一个基础字符串重复组成。

如果它们有共同的基础字符串，那么拼接顺序不应该影响结果。

比如：

```python
str1 = "ABCABC"
str2 = "ABC"
```

那么：

```python
str1 + str2 = "ABCABCABC"
str2 + str1 = "ABCABCABC"
```

两个结果一样，说明有共同重复结构。

但是：

```python
str1 = "LEET"
str2 = "CODE"
```

那么：

```python
str1 + str2 = "LEETCODE"
str2 + str1 = "CODELEET"
```

两个结果不一样，说明没有共同重复结构，所以直接返回：

```python
""
```

---

### 2. 记录两个字符串的长度

```python
a = len(str1)
b = len(str2)
```

这里的 `a` 和 `b` 分别表示两个字符串的长度。

比如：

```python
str1 = "ABABAB"
str2 = "ABAB"
```

那么：

```python
a = 6
b = 4
```

---

### 3. 用辗转相除法求最大公约数

```python
while b != 0:
    old_a = a
    old_b = b

    a = old_b
    b = old_a % old_b
```

这段代码是在求 `a` 和 `b` 的最大公约数。

这里用到的是：

```text
辗转相除法 / Euclidean Algorithm
```

它的核心思想是：

```text
新的 a = 旧的 b
新的 b = 旧的 a % 旧的 b
```

其中：

```python
old_a % old_b
```

表示 `old_a` 除以 `old_b` 的余数。

---

### 4. 以 6 和 4 为例

初始：

```python
a = 6
b = 4
```

第一轮：

```text
旧的 a = 6
旧的 b = 4

新的 a = 旧的 b = 4
新的 b = 旧的 a % 旧的 b = 6 % 4 = 2
```

所以第一轮结束后：

```python
a = 4
b = 2
```

第二轮：

```text
旧的 a = 4
旧的 b = 2

新的 a = 旧的 b = 2
新的 b = 旧的 a % 旧的 b = 4 % 2 = 0
```

所以第二轮结束后：

```python
a = 2
b = 0
```

当 `b = 0` 的时候：

```python
while b != 0:
```

这个循环就会停止。

最后的 `a = 2`，所以：

```python
gcd_length = 2
```

---

### 5. 保存最大公约数长度

```python
gcd_length = a
```

循环结束后，`a` 就是两个字符串长度的最大公约数。

我们把它保存到 `gcd_length` 里面。

比如：

```python
len("ABABAB") = 6
len("ABAB") = 4
```

最大公约数是：

```python
gcd_length = 2
```

---

### 6. 返回答案

```python
return str1[:gcd_length]
```

这句的意思是：

从 `str1` 里面取前 `gcd_length` 个字符。

比如：

```python
str1 = "ABABAB"
gcd_length = 2
```

那么：

```python
str1[:2]
```

得到：

```python
"AB"
```

所以最终返回：

```python
"AB"
```

---

## 复盘 / Review

这题的核心套路是：

```text
如果两个字符串有共同重复结构，那么 str1 + str2 == str2 + str1
```

然后答案长度是：

```text
两个字符串长度的最大公约数
```

以后看到这种题目关键词：

```text
divides string
repeated string
greatest common divisor
```

可以先想到：

```text
字符串拼接判断 + 最大公约数
```

这题最关键的地方不是暴力枚举所有子字符串，而是发现：

```text
共同字符串的长度一定要同时整除 str1 和 str2 的长度
```

所以可以用最大公约数直接找到最长答案。
````
