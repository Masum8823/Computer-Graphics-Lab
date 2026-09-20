# Bresenham Line Drawing Algorithm

> **Bresenham Line Algorithm** হলো computer graphics-এ দুটি point-এর মধ্যে line draw করার একটি efficient algorithm।

DDA-এর সাথে এর সবচেয়ে important difference:

```text
DDA        → Floating Point calculation
Bresenham  → Integer calculation
```

তাই Bresenham সাধারণত DDA-এর চেয়ে **faster এবং efficient**।

---

# 1. Bresenham কী করে?

ধরি আমাদের দুটি point:

```text
Start Point → (x1, y1)

End Point   → (x2, y2)
```

Bresenham এই দুই point-এর মধ্যে কোন কোন pixel/point plot করতে হবে সেটা calculate করে।

সহজভাবে:

```text
Start
  ↓
Next pixel choose
  ↓
Next pixel choose
  ↓
Next pixel choose
  ↓
End
```

---
# 2. DDA-এর সাথে Main Difference

### DDA:

```text
dx
dy
steps
xIncrement
yIncrement
```

এবং decimal value ব্যবহার করে।

### Bresenham:

```text
dx
dy
Decision Parameter
```

এবং মূলত **integer calculation** ব্যবহার করে।

মনে রাখবে:

> **DDA → Floating Point**
> **Bresenham → Integer**

---


# 3. Bresenham-এর Basic Idea

ধরি line-এর slope:

```text
0 < m < 1
```

অর্থাৎ line খুব বেশি steep না।

তাহলে X direction-এ আমরা প্রতিবার:

```text
x = x + 1
```

করব।

কিন্তু Y কখন বাড়বে?

এই দুইটা option থাকবে:

```text
(x+1, y)
```

অথবা:

```text
(x+1, y+1)
```

Bresenham একটি **decision parameter `p`** ব্যবহার করে decide করে কোন point নিতে হবে।

---


# 4. Example

ধরি:

```text
Start = (2,2)

End = (8,5)
```

তাহলে:

```text
dx = 8 - 2 = 6

dy = 5 - 2 = 3
```

এখন প্রতিটি X step-এ Y হয়:

```text
same y
```

অথবা:

```text
y + 1
```

Bresenham `p` দেখে সিদ্ধান্ত নেয়।

---

# 5. Formula

যদি:

```text
dx > dy
```

তাহলে:

```text
p = 2dy - dx
```

এটাই initial decision parameter।

---
# 6. যদি `p < 0`

যদি:

```text
p < 0
```

তাহলে আমরা:

```text
(x+1, y)
```

point নেব।

অর্থাৎ:

```text
x বাড়বে
y একই থাকবে
```

তারপর:

```text
p = p + 2dy
```

---

# 7. যদি `p >= 0`

যদি:

```text
p >= 0
```

তাহলে:

```text
(x+1, y+1)
```

point নেব।

অর্থাৎ:

```text
x বাড়বে
y-ও বাড়বে
```

তারপর:

```text
p = p + 2dy - 2dx
```

---
# 8. Main Logic

এটা খুব ভালো করে বুঝবে:

```text
p < 0
 ↓
(x+1, y)
 ↓
p = p + 2dy


p >= 0
 ↓
(x+1, y+1)
 ↓
p = p + 2dy - 2dx
```

এটাই Bresenham-এর main logic।

---
