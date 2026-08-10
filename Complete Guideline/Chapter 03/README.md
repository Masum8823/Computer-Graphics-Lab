# OpenGL 2D Coordinate System

> OpenGL-এ কোনো Point বা Shape কোথায় আঁকতে হবে সেটা Coordinate দিয়ে নির্ধারণ করা হয়।

---

## 1. কী শিখবো?

এই file-এ আমরা শিখবো:

* Coordinate System কী
* `(x, y)` কী
* `(0, 0)` কোথায়
* `x` এবং `y` কীভাবে কাজ করে
* Positive ও Negative Coordinate
* `glVertex2f(x, y)` কীভাবে বুঝবো
* Point কোথায় হবে সেটা দ্রুত বের করার Trick

---

# 2. Coordinate System কী?

Coordinate System ব্যবহার করে Screen-এর কোনো নির্দিষ্ট জায়গা চিহ্নিত করা হয়।

OpenGL-এর 2D drawing-এ আমরা সাধারণত:

```cpp
glVertex2f(x, y);
```

ব্যবহার করি।

এখানে:

```text
x → Horizontal Position
y → Vertical Position
```

অর্থাৎ:

> `x` বলে Point কতটা **বামে বা ডানে** যাবে।

> `y` বলে Point কতটা **উপরে বা নিচে** যাবে।

---

# 3. OpenGL Coordinate System

Basic OpenGL coordinate system সাধারণভাবে এমন:

```text
                       +Y
                        ↑
                        |
                        |
                        |
              (-)       |       (+)
                        |
          -X  ←---------+---------→  +X
                       (0,0)
                        |
                        |
                        |
                        ↓
                       -Y
```

এখানে Screen-এর Center:

```text
(0,0)
```

---

# 4. `(0,0)` কী?

```cpp
glVertex2f(0.0, 0.0);
```

এখানে:

```text
x = 0
y = 0
```

এটি হলো Coordinate System-এর **Origin**।

সহজভাবে:

> `(0,0)` = Center

```text
+---------------------------+
|                           |
|                           |
|            (0,0)          |
|              ●            |
|                           |
|                           |
+---------------------------+
```

---

# 5. X-Axis

X-axis হলো **Horizontal Line**।

```text
        -X              0              +X
         ←--------------|--------------→
                        |
```

### X-এর value:

```text
Negative X → Left

Positive X → Right
```

উদাহরণ:

```cpp
glVertex2f(-0.5, 0.0);
```

Point হবে Center-এর **বাম দিকে**।

আর:

```cpp
glVertex2f(0.5, 0.0);
```

Point হবে Center-এর **ডান দিকে**।

---

# 6. Y-Axis

Y-axis হলো **Vertical Line**।

```text
                       +Y
                        ↑
                        |
                        |
                        0
                        |
                        |
                        ↓
                       -Y
```

### Y-এর value:

```text
Positive Y → Up

Negative Y → Down
```

উদাহরণ:

```cpp
glVertex2f(0.0, 0.5);
```

Point হবে Center-এর **উপরে**।

আর:

```cpp
glVertex2f(0.0, -0.5);
```

Point হবে Center-এর **নিচে**।

---

# 7. চারটি Quadrant

Coordinate System-কে চারটি অংশে ভাগ করলে:

```text
                    +Y
                     ↑
             II      |       I
                     |
        (-,+)        |       (+,+)
                     |
     -X -------------+------------- +X
                   (0,0)
                     |
             III     |       IV
                     |
        (-,-)        |       (+,-)
                     |
                     ↓
                    -Y
```

---

## Quadrant I

```text
(+x, +y)
```

অর্থাৎ:

> **উপরে ডানদিকে**

Example:

```cpp
glVertex2f(0.5, 0.5);
```

---

## Quadrant II

```text
(-x, +y)
```

অর্থাৎ:

> **উপরে বামদিকে**

Example:

```cpp
glVertex2f(-0.5, 0.5);
```

---

## Quadrant III

```text
(-x, -y)
```

অর্থাৎ:

> **নিচে বামদিকে**

Example:

```cpp
glVertex2f(-0.5, -0.5);
```

---

## Quadrant IV

```text
(+x, -y)
```

অর্থাৎ:

> **নিচে ডানদিকে**

Example:

```cpp
glVertex2f(0.5, -0.5);
```

---

# 8. সবচেয়ে Important Table

| X   | Y   | Point কোথায়? |
| --- | --- | ------------ |
| `+` | `+` | উপরে ডান     |
| `-` | `+` | উপরে বাম     |
| `-` | `-` | নিচে বাম     |
| `+` | `-` | নিচে ডান     |
| `0` | `0` | Center       |

এই Table-টা ভালো করে মনে রাখবে।

---

# 9. `glVertex2f(x, y)` কীভাবে পড়বো?

ধরো:

```cpp
glVertex2f(-0.5, 0.5);
```

প্রথমে:

```text
x = -0.5
```

`x` negative → **বামে**

তারপর:

```text
y = 0.5
```

`y` positive → **উপরে**

তাই:

```text
(-0.5, 0.5)
```

হবে:

> **উপরে বাম দিকে**

---

# 10. কিছু Example

### Example 1

```cpp
glVertex2f(0.5, 0.5);
```

```text
x = +
y = +
```

→ **উপরে ডান**

---

### Example 2

```cpp
glVertex2f(-0.5, 0.5);
```

```text
x = -
y = +
```

→ **উপরে বাম**

---

### Example 3

```cpp
glVertex2f(-0.5, -0.5);
```

```text
x = -
y = -
```

→ **নিচে বাম**

---

### Example 4

```cpp
glVertex2f(0.5, -0.5);
```

```text
x = +
y = -
```

→ **নিচে ডান**

---

# 11. Line-এর Coordinate বুঝি

আমাদের আগের Line code:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

প্রথম Point:

```text
(-0.5, 0)
```

→ Center-এর বামে।

দ্বিতীয় Point:

```text
(0.5, 0)
```

→ Center-এর ডানে।

তাই দুই Point-এর মধ্যে একটি **Horizontal Line** তৈরি হবে।

```text
(-0.5,0) ●────────────● (0.5,0)
```

---

# 12. Triangle-এর Coordinate বুঝি

আগের Triangle:

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

Coordinate:

```text
             (0,0.5)
                ●
               / \
              /   \
             /     \
            /       \
           ●---------●
     (-0.5,-0.5)  (0.5,-0.5)
```

এখানে:

```text
Top       → (0, 0.5)

Bottom Left  → (-0.5, -0.5)

Bottom Right → (0.5, -0.5)
```

এই তিনটি Point যুক্ত করলেই Triangle।

---

# 13. Rectangle-এর Coordinate বুঝি

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

Coordinate:

```text
(-0.5,0.5) ●────────────● (0.5,0.5)
            │            │
            │            │
            │            │
(-0.5,-0.5)●────────────● (0.5,-0.5)
```

তাই:

```text
Top Left     → (-0.5, 0.5)

Top Right    → (0.5, 0.5)

Bottom Right → (0.5, -0.5)

Bottom Left  → (-0.5, -0.5)
```

---
# 14. Circle-এর Coordinate

Circle আঁকার সময় আমরা যে Formula ব্যবহার করেছি:

```text
x = CenterX + Radius × cos(angle)

y = CenterY + Radius × sin(angle)
```

এখানে:

```text
CenterX → Circle-এর বাম/ডান position

CenterY → Circle-এর উপর/নিচ position

Radius → Circle-এর Size
```

যেমন:

```cpp
float x = -0.1 + 0.25 * cos(angle);
float y =  0.0 + 0.25 * sin(angle);
```

তাহলে:

```text
Center = (-0.1, 0.0)

Radius = 0.25
```

অর্থাৎ Circle-এর Center `(0,0)` থেকে একটু বামে।

---

# 15. Coordinate-এর Value যত বেশি হবে?

ধরো:

```cpp
glVertex2f(0.1, 0.1);
```

Point Center-এর খুব কাছে।

কিন্তু:

```cpp
glVertex2f(0.8, 0.8);
```

Point অনেক দূরে **উপরে ডানদিকে** যাবে।

অর্থাৎ:

```text
0.1 → Center-এর কাছে

0.5 → মাঝামাঝি

0.9 → Edge-এর কাছাকাছি
```

Basic OpenGL setup-এ সাধারণত `-1.0` থেকে `+1.0` range-এর মধ্যে coordinate ব্যবহার করা হয়।

---

# 16. `glVertex2f()`-এর `2f` কী?

```cpp
glVertex2f(x, y);
```

এখানে:

```text
2 → 2D Coordinate

f → float
```

তাই `glVertex2f()` মানে:

> Float type-এর 2D coordinate দেওয়ার function।

---

# 17. Common Mistake

### Mistake 1: X এবং Y উল্টে ফেলা

```cpp
glVertex2f(-0.5, 0.5);
```

এখানে:

```text
X = -0.5 → Left
Y = +0.5 → Up
```

তাই **Top Left**।

---

### Mistake 2: Y-axis-এর direction ভুল মনে করা

OpenGL-এর basic 2D coordinate-এ:

```text
+y → Up

-y → Down
```

তাই:

```cpp
glVertex2f(0.0, 0.5);
```

→ Up

এবং:

```cpp
glVertex2f(0.0, -0.5);
```

→ Down

---


# 18. Viva Questions

### Q1. OpenGL-এ `(0,0)` কী?

**Answer:** এটি হলো Origin, যা basic 2D coordinate system-এর Center হিসেবে ধরা হয়।

---

### Q2. Positive X কোন দিকে?

**Answer:** Right দিকে।

---

### Q3. Negative X কোন দিকে?

**Answer:** Left দিকে।

---

### Q4. Positive Y কোন দিকে?

**Answer:** Up দিকে।

---

### Q5. Negative Y কোন দিকে?

**Answer:** Down দিকে।

---

### Q6. `glVertex2f()` কী কাজ করে?

**Answer:** 2D float coordinate নির্ধারণ করে।

---

### Q7. `glVertex2f(0.5,0.5)` কোথায় Point তৈরি করবে?

**Answer:** Center-এর **উপরে ডানদিকে**।

---

### Q8. `glVertex2f(-0.5,-0.5)` কোথায় Point তৈরি করবে?

**Answer:** Center-এর **নিচে বামদিকে**।

---

### Q9. `glVertex2f(-0.5,0.5)` কোথায় Point তৈরি করবে?

**Answer:** Center-এর **উপরে বামদিকে**।

---

### Q10. `glVertex2f(0.5,-0.5)` কোথায় Point তৈরি করবে?

**Answer:** Center-এর **নিচে ডানদিকে**।

---
