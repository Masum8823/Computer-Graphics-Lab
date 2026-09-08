# Draw Japan Flag

> OpenGL-এ basic shapes ব্যবহার করে Japan-এর national flag আঁকা।

---

# 1. Japan Flag কীভাবে বানাবো?

Japan-এর Flag খুব simple:

```text
White Rectangle
      +
Red Circle
      ↓
Japan Flag
```

দেখতে:

```text
┌──────────────────────────────┐
│                              │
│             ●                │
│                              │
└──────────────────────────────┘
```

এখানে:

```text
White → Background
Red   → Circle
```

---


# 2. Basic Code

```cpp
#include <GL/glut.h>
#include <math.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // =========================
    // White Flag Background
    // =========================

    glColor3f(1.0, 1.0, 1.0);

    glBegin(GL_QUADS);

    glVertex2f(-0.8, 0.5);
    glVertex2f(0.8, 0.5);
    glVertex2f(0.8, -0.5);
    glVertex2f(-0.8, -0.5);

    glEnd();


    // =========================
    // Red Circle
    // =========================

    glColor3f(1.0, 0.0, 0.0);

    glBegin(GL_POLYGON);

    for(int i = 0; i < 360; i++)
    {
        float angle = i * 3.1416 / 180.0;

        float x = 0.0 + 0.25 * cos(angle);
        float y = 0.0 + 0.25 * sin(angle);

        glVertex2f(x, y);
    }

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Japan Flag");

    // White Background
    glClearColor(0.7, 0.7, 0.7, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 3. প্রথমে White Rectangle

Japan Flag-এর main অংশ হলো একটা Rectangle।

তাই:

```cpp
glBegin(GL_QUADS);
```

ব্যবহার করেছি।

কারণ:

```text
Rectangle
   ↓
GL_QUADS
```

---


# 4. Rectangle-এর Color

```cpp
glColor3f(1.0, 1.0, 1.0);
```

মানে:

```text
R = 1
G = 1
B = 1
```

তাই:

> White

হবে।

---


# 5. Rectangle-এর চারটি Vertex

```cpp
glVertex2f(-0.8, 0.5);
glVertex2f(0.8, 0.5);
glVertex2f(0.8, -0.5);
glVertex2f(-0.8, -0.5);
```

চারটি point:

```text
Top Left     = (-0.8, 0.5)

Top Right    = (0.8, 0.5)

Bottom Right = (0.8, -0.5)

Bottom Left  = (-0.8, -0.5)
```

এগুলো connect করলে White Rectangle হবে।

---


# 6. Coordinate দিয়ে বুঝি

```text
(-0.8,0.5) ---------------- (0.8,0.5)
      |                         |
      |       WHITE FLAG        |
      |                         |
(-0.8,-0.5) -------------- (0.8,-0.5)
```

---

# 7. এবার Red Circle

এখন Flag-এর মাঝখানে Red Circle দিতে হবে।

```cpp
glColor3f(1.0, 0.0, 0.0);
```

এটা:

```text
R = 1
G = 0
B = 0
```

তাই:

> Red

Color হবে।

---

# 8. Circle-এর জন্য `GL_POLYGON`

```cpp
glBegin(GL_POLYGON);
```

ব্যবহার করছি।

আগের Circle-এর মতো অনেকগুলো point তৈরি করে Polygon বানাচ্ছি।

```text
Many Points
     ↓
GL_POLYGON
     ↓
Circle
```

---

# 9. `for` Loop

```cpp
for(int i = 0; i < 360; i++)
```

মানে:

```text
0°
 থেকে
359°
```

পর্যন্ত ঘুরবে।

প্রতিটি angle-এর জন্য একটা point তৈরি হবে।

---

# 10. Angle

```cpp
float angle = i * 3.1416 / 180.0;
```

এটা:

```text
Degree
   ↓
Radian
```

এ convert করছে।

কারণ `sin()` এবং `cos()` দিয়ে Circle বানানোর সময় Radian ব্যবহার করছি।

---

# 11. Red Circle-এর X Coordinate

```cpp
float x = 0.0 + 0.25 * cos(angle);
```

এখানে:

```text
0.0 → Center X

0.25 → Radius
```

তাই:

```text
Center X = 0.0
Radius = 0.25
```

---

# 12. Red Circle-এর Y Coordinate

```cpp
float y = 0.0 + 0.25 * sin(angle);
```

এখানে:

```text
0.0 → Center Y

0.25 → Radius
```

তাই:

```text
Center Y = 0.0
Radius = 0.25
```

---

# 13. Circle-এর Center

দুটো line একসাথে:

```cpp
float x = 0.0 + 0.25 * cos(angle);
float y = 0.0 + 0.25 * sin(angle);
```

তাই Circle-এর center:

```text
(0.0, 0.0)
```

অর্থাৎ Flag-এর একদম center-এ।

---

# 14. Circle-এর Radius

এখানে:

```text
0.25
```

হলো Radius।

তাই:

```text
Center = (0.0, 0.0)

Radius = 0.25
```

---

# 15. `glVertex2f(x,y)`

```cpp
glVertex2f(x, y);
```

প্রতিবার Circle-এর একটি point তৈরি করছে।

Flow:

```text
angle
  ↓
cos / sin
  ↓
x, y
  ↓
glVertex2f(x,y)
  ↓
Point
```

360 বার করলে অনেক point তৈরি হবে।

তারপর:

```text
Many Points
     ↓
GL_POLYGON
     ↓
Circle
```

---

# 16. কেন Circle-এর Center `(0,0)`?

Bangladesh Flag-এর ক্ষেত্রে আমরা:

```cpp
x = -0.1 + ...
```

ব্যবহার করেছিলাম।

তাই Circle একটু Left-এ ছিল।

কিন্তু Japan Flag-এর Circle সাধারণভাবে মাঝখানে থাকে।

তাই:

```cpp
x = 0.0 + ...
y = 0.0 + ...
```

ব্যবহার করেছি।

অর্থাৎ:

```text
Center X = 0
Center Y = 0
```

---


# 17. Bangladesh Flag vs Japan Flag

দুটোই একই concept:

```text
Rectangle + Circle
```

কিন্তু Circle-এর position আলাদা।

### Bangladesh:

```cpp
float x = -0.1 + 0.25 * cos(angle);
float y = 0.0 + 0.25 * sin(angle);
```

Circle একটু Left-এ।

### Japan:

```cpp
float x = 0.0 + 0.25 * cos(angle);
float y = 0.0 + 0.25 * sin(angle);
```

Circle Center-এ।

---


# 18. Japan Flag-এর Main Structure

```text
White Rectangle
       +
Red Circle
       ↓
Japan Flag
```

অর্থাৎ:

```text
Rectangle → GL_QUADS

Circle → GL_POLYGON
         ↓
      sin/cos
```

---


# 19. Circle বড় করতে চাইলে

বর্তমানে:

```cpp
0.25
```

হলো Radius।

যদি:

```cpp
float x = 0.0 + 0.35 * cos(angle);
float y = 0.0 + 0.35 * sin(angle);
```

দাও:

```text
Radius = 0.35
```

তাহলে Circle বড় হবে।

---


# 20. Circle ছোট করতে চাইলে

```cpp
float x = 0.0 + 0.15 * cos(angle);
float y = 0.0 + 0.15 * sin(angle);
```

তাহলে:

```text
Radius = 0.15
```

Circle ছোট হবে।

---

# 21. Circle Right দিকে নিতে চাইলে

```cpp
float x = 0.1 + 0.25 * cos(angle);
```

তাহলে:

```text
Center X = 0.1
```

Circle Right দিকে যাবে।

কারণ:

```text
+X → Right
```

---

# 22. Circle Left দিকে নিতে চাইলে

```cpp
float x = -0.1 + 0.25 * cos(angle);
```

তাহলে Circle Left দিকে যাবে।

কারণ:

```text
-X → Left
```

---
# 23. Circle উপরে নিতে চাইলে

```cpp
float y = 0.2 + 0.25 * sin(angle);
```

তাহলে:

```text
Center Y = 0.2
```

Circle উপরে যাবে।

কারণ:

```text
+Y → Up
```

---


# 24. Circle নিচে নিতে চাইলে

```cpp
float y = -0.2 + 0.25 * sin(angle);
```

তাহলে Circle নিচে যাবে।

কারণ:

```text
-Y → Down
```

---

# 25. Flag-এর Size Change

বর্তমানে:

```text
X = -0.8 → 0.8

Y = -0.5 → 0.5
```

Width:

```text
0.8 - (-0.8) = 1.6
```

Height:

```text
0.5 - (-0.5) = 1.0
```

---

# 26. Flag Width বাড়ানো

```cpp
glVertex2f(-0.9, 0.5);
glVertex2f(0.9, 0.5);
glVertex2f(0.9, -0.5);
glVertex2f(-0.9, -0.5);
```

এতে Flag আরও wide হবে।

---

# 27. Flag Height বাড়ানো

```cpp
glVertex2f(-0.8, 0.6);
glVertex2f(0.8, 0.6);
glVertex2f(0.8, -0.6);
glVertex2f(-0.8, -0.6);
```

এতে Flag আরও tall হবে।

---


# 28. Background Color

Code-এ:

```cpp
glClearColor(0.7, 0.7, 0.7, 1.0);
```

দিয়েছি।

এটা Window-এর background gray করবে।

কারণ Flag-এর background নিজেই White Rectangle।

তাই:

```text
Window Background → Gray

Flag Background → White
```

এতে White Flag-এর boundary সহজে দেখা যাবে।

---

# 29. কেন `glClearColor()` White না দিয়ে Gray?

যদি:

```cpp
glClearColor(1.0, 1.0, 1.0, 1.0);
```

দাও, তাহলে:

```text
Window Background = White
Flag = White
```

দুটো একই color হয়ে যাবে।

তখন Flag-এর White অংশ আলাদা করে বোঝা কঠিন হতে পারে।

তাই demonstration-এর জন্য:

```cpp
glClearColor(0.7, 0.7, 0.7, 1.0);
```

দিয়েছি।

---

# 30. Full Drawing Logic

```text
glClear()
   ↓
White Color
   ↓
GL_QUADS
   ↓
White Rectangle
   ↓
Red Color
   ↓
GL_POLYGON
   ↓
360 Points
   ↓
Red Circle
   ↓
glFlush()
```

---

# 31. Exam-এ কীভাবে চিনবে?

Question যদি আসে:

> Draw Japan Flag using OpenGL

তাহলে সাথে সাথে মনে করবে:

```text
Japan Flag
    ↓
White Rectangle
    +
Red Circle
```

তারপর:

```text
Rectangle → GL_QUADS

Circle → GL_POLYGON
         ↓
       sin/cos
```

---

# 32. সবচেয়ে Important Part

Exam-এর সময় এই অংশটা ভালোভাবে বুঝে রাখবে:

```cpp
// White Rectangle
glColor3f(1.0, 1.0, 1.0);

glBegin(GL_QUADS);

glVertex2f(-0.8, 0.5);
glVertex2f(0.8, 0.5);
glVertex2f(0.8, -0.5);
glVertex2f(-0.8, -0.5);

glEnd();


// Red Circle
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POLYGON);

for(int i = 0; i < 360; i++)
{
    float angle = i * 3.1416 / 180.0;

    float x = 0.0 + 0.25 * cos(angle);
    float y = 0.0 + 0.25 * sin(angle);

    glVertex2f(x, y);
}

glEnd();
```

---


# 33. Viva Questions

### Q1. Japan Flag কী দিয়ে তৈরি?

**Answer:** একটি White Rectangle এবং একটি Red Circle দিয়ে।

---

### Q2. Rectangle-এর জন্য কোন primitive?

**Answer:** `GL_QUADS`।

---

### Q3. Circle-এর জন্য কোন primitive?

**Answer:** `GL_POLYGON`।

---

### Q4. Circle-এর Center কত?

**Answer:**

```text
(0.0, 0.0)
```

---

### Q5. Circle-এর Radius কত?

**Answer:**

```text
0.25
```

---

### Q6. Circle-এর X coordinate formula কী?

**Answer:**

```text
x = centerX + radius × cos(angle)
```

---

### Q7. Circle-এর Y coordinate formula কী?

**Answer:**

```text
y = centerY + radius × sin(angle)
```

---

### Q8. Circle-এর Center `(0,0)` কেন?

**Answer:** Flag-এর মাঝখানে Circle রাখার জন্য।

---

### Q9. Circle বড় করতে কী পরিবর্তন করবো?

**Answer:** Radius-এর value বাড়াবো।

---

### Q10. Japan Flag-কে Composite Shape বলা যায় কেন?

**Answer:** একাধিক basic shape combine করে তৈরি করা হয়েছে।

---

# 34. Common Mistakes

### Mistake 1: Circle-এর Center ভুল করা

Japan Flag-এর জন্য:

```cpp
float x = 0.0 + ...
float y = 0.0 + ...
```

দেওয়া হয়েছে।

তাই:

```text
Center = (0,0)
```

---

### Mistake 2: Radius-কে Center ভাবা

এখানে:

```cpp
0.0 + 0.25 * cos(angle)
```

এর:

```text
0.0 → Center X

0.25 → Radius
```

---

### Mistake 3: `sin()` এবং `cos()` উল্টে ফেলা

মনে রাখবে:

```text
X → cos()

Y → sin()
```

অর্থাৎ:

```cpp
x = centerX + radius * cos(angle);

y = centerY + radius * sin(angle);
```

---

### Mistake 4: `glBegin()` / `glEnd()` ভুলে যাওয়া

Rectangle:

```cpp
glBegin(GL_QUADS);

// vertices

glEnd();
```

Circle:

```cpp
glBegin(GL_POLYGON);

// vertices

glEnd();
```

---
