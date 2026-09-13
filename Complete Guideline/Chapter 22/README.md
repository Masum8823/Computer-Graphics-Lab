# Homogeneous Transformation

> Homogeneous Transformation হলো **2D/3D transformation-কে matrix-এর মাধ্যমে represent করার একটি পদ্ধতি**।

---

# 1. Homogeneous Transformation কী?

আমরা আগের ৩টা Transformation দেখেছি:

```text
Translation → Move
Rotation    → Rotate
Scaling     → Size Change
```

কিন্তু একটা সমস্যা আছে।

Translation-এর formula:

```text
x' = x + Tx
y' = y + Ty
```

এখানে `+` আছে।

অন্যদিকে Scaling:

```text
x' = x × Sx
y' = y × Sy
```

এখানে `×` আছে।

Rotation-এর formula-তেও `sin` এবং `cos` আছে।

এগুলোকে **একটা common matrix format**-এ আনার জন্য আমরা **Homogeneous Coordinates** ব্যবহার করি।

---


# 2. Normal Coordinate

আমরা সাধারণত একটি 2D point লিখি:

```text
(x, y)
```

যেমন:

```text
(2, 3)
```

কিন্তু Homogeneous Coordinate-এ লিখি:

```text
(x, y, 1)
```

তাই:

```text
Normal:

(x, y)


Homogeneous:

(x, y, 1)
```

---
# 3. কেন extra `1`?

এই `1`-এর কারণে Translation-ও matrix multiplication দিয়ে করা সম্ভব হয়।

অর্থাৎ:

```text
(x, y)
```

থেকে:

```text
(x, y, 1)
```

করলে Translation, Rotation এবং Scaling—সবগুলোকে matrix দিয়ে represent করা যায়।

Exam-এর জন্য এই lineটা খুব important:

> **2D homogeneous coordinate-এ একটি point-কে `(x, y, 1)` হিসেবে represent করা হয়।**

---
# 4. Homogeneous Coordinate

ধরি একটি point:

```text
P = (x, y)
```

Homogeneous form:

```text
P = (x, y, 1)
```

Matrix form:

```text
      ┌   ┐
      │ x │
P  =  │ y │
      │ 1 │
      └   ┘
```

---

# 5. Transformation Matrix

Homogeneous coordinate ব্যবহার করে transformation:

```text
P' = T × P
```

এখানে:

```text
P  → Original Point
T  → Transformation Matrix
P' → New Point
```

সহজভাবে:

```text
Original Point
      ↓
Transformation Matrix
      ↓
New Point
```

---


# 6. Translation Matrix

Translation-এর জন্য matrix:

```text
      ┌             ┐
      │ 1   0   Tx  │
T  =  │ 0   1   Ty  │
      │ 0   0   1   │
      └             ┘
```

আর point:

```text
      ┌   ┐
      │ x │
P  =  │ y │
      │ 1 │
      └   ┘
```

তাহলে:

```text
P' = T × P
```

---


# 7. Translation Matrix সহজভাবে

মনে রাখবে:

```text
┌ 1  0  Tx ┐
│ 0  1  Ty │
└ 0  0  1  ┘
```

এখানে:

```text
Tx → X direction movement

Ty → Y direction movement
```

---

# 8. Translation Matrix থেকে Formula

Multiplication করলে:

```text
x' = x + Tx

y' = y + Ty
```

অর্থাৎ আমরা আগে যে formula শিখেছি সেটাই পাওয়া যায়।

---