**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "401. Binary Watch"
date: "2026-02-17"
tags: Easy
categories:
  - "LeetCode Math"
---


- A binary watch has 4 LEDs on the top to represent the hours (0-11), and 6 LEDs on the bottom to represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.
  - For example, the below binary watch reads `"4:51"`.
- Given an integer `turnedOn` which represents the number of LEDs that are currently on (ignoring the PM), return *all possible times the watch could represent*. You may return the answer in **any order**.
- The hour must not contain a leading zero.
  - For example, `"01:00"` is not valid. It should be `"1:00"`.
- The minute must consist of two digits and may contain a leading zero.
  - For example, `"10:2"` is not valid. It should be `"10:02"`.

**Example 1**

```
Input: turnedOn = 1
Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
```

**Example 2**

```
Input: turnedOn = 9
Output: []
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

import java.util.ArrayList;
import java.util.List;

/**
 * @Author zhengxingxing
 * @Date 2026/02/17
 */
public class BinaryWatch {
    public static List<String> readBinaryWatch(int turnedOn) {
        List<String> ans = new ArrayList<>();
        // There are at most 10 LEDs in total (4 for hours + 6 for minutes)
        if (turnedOn < 0 || turnedOn > 10) {
            return ans;
        }
        // Enumerate all valid times: hour 0~11, minute 0~59
        for (int hour = 0; hour < 12; hour++) {
            for (int minute = 0; minute < 60; minute++) {
                // Integer.bitCount counts the number of 1s in binary representation
                if (Integer.bitCount(hour) + Integer.bitCount(minute) == turnedOn) {
                    // Hour has no leading zero, minute must be two digits
                    ans.add(hour + ":" + (minute < 10 ? "0" + minute : minute));
                }
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        int turnedOn1 = 1;
        int turnedOn2 = 9;
        System.out.println("turnedOn = " + turnedOn1);
        System.out.println(readBinaryWatch(turnedOn1));
        System.out.println("turnedOn = " + turnedOn2);
        System.out.println(readBinaryWatch(turnedOn2));
    }
}
```