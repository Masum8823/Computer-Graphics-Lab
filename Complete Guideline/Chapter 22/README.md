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

# 9. Example

ধরি:

```text
Point = (2, 3)
```

এবং:

```text
Tx = 4
Ty = 2
```

তাহলে:

```text
x' = 2 + 4
   = 6

y' = 3 + 2
   = 5
```

New Point:

```text
(6, 5)
```

---
# 10. Scaling Matrix

Scaling-এর matrix:

```text
      ┌             ┐
S  =  │ Sx  0   0   │
      │ 0   Sy  0   │
      │ 0   0   1   │
      └             ┘
```

এখানে:

```text
Sx → X-axis scaling

Sy → Y-axis scaling
```

---

# 11. Scaling Formula

Matrix multiplication করলে:

```text
x' = x × Sx

y' = y × Sy
```

এটাই আমাদের আগের Scaling-এর formula।

---
# 12. Example

ধরি:

```text
Point = (2, 3)
```

Scaling:

```text
Sx = 2
Sy = 3
```

তাহলে:

```text
x' = 2 × 2
   = 4

y' = 3 × 3
   = 9
```

New Point:

```text
(4, 9)
```

---


# 13. Rotation Matrix

2D Rotation-এর matrix:

```text
      ┌                    ┐
R  =  │ cosθ   -sinθ   0  │
      │ sinθ    cosθ   0  │
      │  0        0    1  │
      └                    ┘
```

এখানে:

```text
θ = Rotation Angle
```

---
# 14. Rotation Formula

Matrix multiplication-এর পরে:

```text
x' = x cosθ - y sinθ

y' = x sinθ + y cosθ
```

এই formula আমরা Rotation-এর notes-এও দেখেছি।

---
# 15. Example: 90° Rotation

ধরি:

```text
Point = (1, 0)
```

এবং:

```text
θ = 90°
```

আমরা জানি:

```text
cos90° = 0

sin90° = 1
```

তাই:

```text
x' = (1 × 0) - (0 × 1)
   = 0

y' = (1 × 1) + (0 × 0)
   = 1
```

New Point:

```text
(0, 1)
```

---
# 16. তিনটি Transformation-এর Matrix

এটা **খুব important**।

### Translation

```text
┌ 1  0  Tx ┐
│ 0  1  Ty │
└ 0  0  1  ┘
```

### Scaling

```text
┌ Sx  0  0 ┐
│ 0  Sy  0 │
└ 0   0  1 │
```

### Rotation

```text
┌ cosθ  -sinθ  0 ┐
│ sinθ   cosθ  0 │
└  0       0   1 │
```

---
# 17. কেন Homogeneous Transformation দরকার?

সব Transformation-কে একই matrix format-এ আনার জন্য।

```text
Translation
     ↓
Matrix

Rotation
     ↓
Matrix

Scaling
     ↓
Matrix
```

তাই একাধিক transformation একসাথে করা সহজ হয়।

---
# 18. Composite Transformation

একাধিক transformation একসাথে করলে তাকে:

> **Composite Transformation**

বলে।

যেমন:

```text
Translation
     +
Rotation
     +
Scaling
```

একসাথে apply করা।

---

# 19. Composite Transformation Example

ধরি একটি object:

```text
1. প্রথমে বড় হবে
2. তারপর rotate হবে
3. তারপর move হবে
```

তাহলে:

```text
Scaling
   ↓
Rotation
   ↓
Translation
```

এগুলো matrix দিয়ে একসাথে represent করা যায়।

---

# 20. Composite Matrix

ধরি:

```text
T = Translation Matrix
R = Rotation Matrix
S = Scaling Matrix
```

তাহলে Composite Transformation:

```text
M = T × R × S
```

এবং:

```text
P' = M × P
```

অর্থাৎ:

```text
P' = T × R × S × P
```

---

# 21. Transformation Order খুব Important

এটা মনে রাখবে:

> **Transformation-এর order change করলে result-ও change হতে পারে।**

যেমন:

```text
Translate → Rotate
```

এবং:

```text
Rotate → Translate
```

একই result নাও হতে পারে।

---
# 22. সহজ Example

ধরি:

```text
Point → (1,0)
```

প্রথমে Rotate:

```text
90°
```

তাহলে:

```text
(1,0) → (0,1)
```

তারপর Translate:

```text
Tx = 2
```

তাহলে:

```text
(0,1) → (2,1)
```

কিন্তু যদি আগে Translate করি:

```text
(1,0) → (3,0)
```

তারপর Rotate করি:

```text
(3,0) → (0,3)
```

দেখতেই পাচ্ছো:

```text
(2,1) ≠ (0,3)
```

তাই:

> **Order matters.**

---
# 23. Homogeneous Coordinate-এর Main Idea

Normal point:

```text
(x, y)
```

কে:

```text
(x, y, 1)
```

করি।

তারপর:

```text
Transformation Matrix
        ×
Homogeneous Point
        ↓
New Point
```

---
# 24. OpenGL-এর সাথে Relation

আমরা আগের notes-এ ব্যবহার করেছি:

```cpp
glTranslatef();
glRotatef();
glScalef();
```

এই function-গুলো internally transformation matrix-এর concept ব্যবহার করে।

যেমন:

```cpp
glTranslatef(0.5, 0.2, 0.0);
```

Translation transformation apply করে।

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

Rotation transformation apply করে।

```cpp
glScalef(2.0, 2.0, 1.0);
```

Scaling transformation apply করে।

---
# 25. `glTranslatef()` বনাম Translation Matrix

OpenGL:

```cpp
glTranslatef(Tx, Ty, 0);
```

Mathematics:

```text
┌ 1  0  Tx ┐
│ 0  1  Ty │
└ 0  0  1  ┘
```

অর্থাৎ একই transformation-এর দুইটা representation।

---

# 26. `glRotatef()` বনাম Rotation Matrix

OpenGL:

```cpp
glRotatef(angle, 0, 0, 1);
```

Mathematics:

```text
┌ cosθ  -sinθ  0 ┐
│ sinθ   cosθ  0 │
└  0       0   1 │
```

---

# 27. `glScalef()` বনাম Scaling Matrix

OpenGL:

```cpp
glScalef(Sx, Sy, 1);
```

Mathematics:

```text
┌ Sx  0   0 ┐
│ 0   Sy  0 │
└ 0   0   1 │
```

---
