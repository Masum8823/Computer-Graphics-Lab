# Draw Bangladesh Flag

> OpenGL-এ basic shapes ব্যবহার করে বাংলাদেশের জাতীয় পতাকা আঁকা।

---

# 1. Bangladesh Flag কীভাবে বানাবো?

বাংলাদেশের Flag খুব সহজে ২টা shape দিয়ে বানানো যায়:

```text
Rectangle → Green Background

Circle → Red Circle
```

অর্থাৎ:

```text
Green Rectangle
       +
 Red Circle
       ↓
Bangladesh Flag
```

---

# 2. Flag দেখতে কেমন?

```text
┌──────────────────────────────┐
│                              │
│             ●                │
│                              │
└──────────────────────────────┘
```

এখানে:

```text
Green → Background
Red   → Circle
```

---

# 3. Basic Code

```cpp
#include <GL/glut.h>
#include <math.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // =========================
    // Green Background
    // =========================

    glColor3f(0.0, 0.5, 0.0);

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

        float x = -0.1 + 0.25 * cos(angle);
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

    glutCreateWindow("Bangladesh Flag");

    // White Background
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 4. প্রথমে Green Rectangle

Flag-এর main part হলো Green Rectangle।

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

# 5. Green Color

```cpp
glColor3f(0.0, 0.5, 0.0);
```

এখানে:

```text
R = 0.0
G = 0.5
B = 0.0
```

তাই Green color হবে।

---

# 6. Rectangle-এর চারটি Vertex

```cpp
glVertex2f(-0.8, 0.5);
glVertex2f(0.8, 0.5);
glVertex2f(0.8, -0.5);
glVertex2f(-0.8, -0.5);
```

এগুলো হলো:

```text
Top Left     = (-0.8, 0.5)

Top Right    = (0.8, 0.5)

Bottom Right = (0.8, -0.5)

Bottom Left  = (-0.8, -0.5)
```

---

# 7. Coordinate দিয়ে বুঝি

```text
(-0.8,0.5) ---------------- (0.8,0.5)
      |                         |
      |      GREEN FLAG         |
      |                         |
(-0.8,-0.5) -------------- (0.8,-0.5)
```

এটাই Flag-এর Green Background।

---

# 8. Rectangle শেষ

```cpp
glEnd();
```

এখন:

```text
┌──────────────────────┐
│                      │
│      GREEN FLAG      │
│                      │
└──────────────────────┘
```

তৈরি হয়েছে।

---
# 9. এবার Red Circle

এবার Flag-এর মধ্যে Red Circle দিতে হবে।

তাই:

```cpp
glColor3f(1.0, 0.0, 0.0);
```

মানে:

```text
R = 1
G = 0
B = 0
```

অর্থাৎ Red।

---

# 10. Circle-এর জন্য `GL_POLYGON`

আমরা আগের Circle-এর মতো:

```cpp
glBegin(GL_POLYGON);
```

ব্যবহার করছি।

কারণ Circle আমরা অনেকগুলো ছোট point দিয়ে Polygon-এর মতো বানাচ্ছি।

```text
Many Points
     ↓
GL_POLYGON
     ↓
Circle
```

---

# 11. `for` Loop

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

প্রতিটি angle-এর জন্য একটি point তৈরি হবে।

---


# 12. Angle Calculation

```cpp
float angle = i * 3.1416 / 180.0;
```

এখানে:

```text
Degree
  ↓
Radian
```

এ convert করা হচ্ছে।

কারণ `sin()` এবং `cos()` সাধারণত Radian ব্যবহার করে।

---

# 13. Red Circle-এর X Coordinate

```cpp
float x = -0.1 + 0.25 * cos(angle);
```

এখানে:

```text
-0.1 → Center X

0.25 → Radius
```

তাই:

```text
Circle Center X = -0.1
Radius = 0.25
```

---
# 14. Red Circle-এর Y Coordinate

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
Circle Center Y = 0.0
Radius = 0.25
```

---

# 15. Circle-এর Center

আমাদের:

```cpp
float x = -0.1 + 0.25 * cos(angle);
float y = 0.0 + 0.25 * sin(angle);
```

তাই Circle-এর center:

```text
(-0.1, 0.0)
```

---

# 16. Circle-এর Radius

এখানে:

```text
0.25
```

হলো Radius।

তাই:

```text
Center = (-0.1, 0.0)

Radius = 0.25
```

---

# 17. `glVertex2f(x,y)`

```cpp
glVertex2f(x, y);
```

প্রতিবার Circle-এর একটি নতুন point তৈরি করছে।

```text
angle
 ↓
cos/sin
 ↓
x,y
 ↓
glVertex2f()
 ↓
Point
```

360 বার করলে অনেকগুলো point পাওয়া যায়।

তারপর:

```text
Many Points
     ↓
GL_POLYGON
     ↓
Circle
```

---

# 18. Circle-এর Position কেন `-0.1`?

এটা খুব important।

যদি লিখতাম:

```cpp
float x = 0.0 + 0.25 * cos(angle);
```

তাহলে Circle একদম center-এ থাকতো।

কিন্তু:

```cpp
float x = -0.1 + 0.25 * cos(angle);
```

দেওয়ায় Circle একটু **Left side-এ** চলে যায়।

কারণ:

```text
-X → Left
```

তাই:

```text
-0.1
```

দেওয়া হয়েছে।

---


# 19. কেন `y = 0.0`?

```cpp
float y = 0.0 + 0.25 * sin(angle);
```

এখানে Center Y:

```text
0.0
```

তাই Circle vertically center-এর কাছাকাছি থাকবে।

---

# 20. Flag-এর Complete Structure

```text
                 Green Rectangle
┌──────────────────────────────────┐
│                                  │
│             🔴                   │
│                                  │
└──────────────────────────────────┘
```

Conceptually:

```text
Green Rectangle
       +
Red Circle
       ↓
Bangladesh Flag
```

---

# 21. কোন অংশে কোন Primitive?

এটা অবশ্যই মনে রাখবে:

```text
Green Background
      ↓
GL_QUADS

Red Circle
      ↓
GL_POLYGON
      ↓
sin() + cos()
```

---


# 22. কেন Rectangle আগে আঁকছি?

আমরা প্রথমে:

```text
Green Rectangle
```

আঁকছি।

তারপর তার উপরে:

```text
Red Circle
```

আঁকছি।

OpenGL-এ পরের shape আগের shape-এর উপরে দেখা যায়।

তাই:

```text
1st → Green Rectangle

2nd → Red Circle
```

ফলে Red Circle Green-এর উপর দেখা যায়।

---

# 23. Red Circle বড় করতে চাইলে

বর্তমানে:

```cpp
0.25
```

হলো Radius।

যদি:

```cpp
float x = -0.1 + 0.3 * cos(angle);
float y = 0.0 + 0.3 * sin(angle);
```

দাও:

```text
Radius = 0.3
```

তাহলে Circle বড় হবে।

---
# 24. Red Circle ছোট করতে চাইলে

```cpp
float x = -0.1 + 0.15 * cos(angle);
float y = 0.0 + 0.15 * sin(angle);
```

তাহলে:

```text
Radius = 0.15
```

Circle ছোট হবে।

---

# 25. Red Circle Right দিকে নিতে চাইলে

বর্তমানে:

```cpp
-0.1
```

আছে।

এটা:

```cpp
0.1
```

করলে:

```cpp
float x = 0.1 + 0.25 * cos(angle);
```

Circle Right দিকে যাবে।

কারণ:

```text
+X → Right
```

---

# 26. Red Circle Left দিকে নিতে চাইলে

যেমন:

```cpp
float x = -0.2 + 0.25 * cos(angle);
```

তাহলে Circle আরও Left দিকে যাবে।

কারণ:

```text
-X → Left
```

---

# 27. Red Circle উপরে নিতে চাইলে

বর্তমানে:

```cpp
float y = 0.0 + 0.25 * sin(angle);
```

যদি:

```cpp
float y = 0.2 + 0.25 * sin(angle);
```

দাও:

```text
Center Y = 0.2
```

তাই Circle উপরে যাবে।

কারণ:

```text
+Y → Up
```

---

# 28. Red Circle নিচে নিতে চাইলে

```cpp
float y = -0.2 + 0.25 * sin(angle);
```

তাহলে:

```text
Center Y = -0.2
```

এবং Circle নিচে যাবে।

---


# 29. Flag-এর Size Change

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

তাই Flag-এর ratio:

```text
1.6 : 1.0
```

---

# 30. Flag Width বাড়াতে চাইলে

```cpp
glVertex2f(-0.9, 0.5);
glVertex2f(0.9, 0.5);
glVertex2f(0.9, -0.5);
glVertex2f(-0.9, -0.5);
```

এতে Flag আরও wide হবে।

---

# 31. Flag Height বাড়াতে চাইলে

যেমন:

```cpp
glVertex2f(-0.8, 0.6);
glVertex2f(0.8, 0.6);
glVertex2f(0.8, -0.6);
glVertex2f(-0.8, -0.6);
```

তাহলে Flag taller হবে।

---

# 32. Green-এর Color Change

বর্তমানে:

```cpp
glColor3f(0.0, 0.5, 0.0);
```

এখানে Green-এর intensity বাড়াতে চাইলে:

```cpp
glColor3f(0.0, 0.8, 0.0);
```

দিতে পারো।

তবে Lab-এর জন্য basic value মনে রাখলেই হবে।

---

# 33. Red Circle-এর Color

```cpp
glColor3f(1.0, 0.0, 0.0);
```

এটা pure Red।

```text
R = 1
G = 0
B = 0
```

---

# 34. পুরো Code-এর Logic

```text
glClear()
   ↓
Green Color Set
   ↓
GL_QUADS
   ↓
Green Rectangle
   ↓
Red Color Set
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

# 35. Exam-এ কীভাবে ভাববে?

Question:

> **Draw Bangladesh Flag using OpenGL**

সাথে সাথে মনে করবে:

```text
Bangladesh Flag
      ↓
Green Rectangle
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

# 36. সবচেয়ে Important Code

Exam-এর সময় মূল অংশটা:

```cpp
// Green Rectangle
glColor3f(0.0, 0.5, 0.0);

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

    float x = -0.1 + 0.25 * cos(angle);
    float y = 0.0 + 0.25 * sin(angle);

    glVertex2f(x, y);
}

glEnd();
```

এই অংশটা ভালোভাবে বুঝে রাখলে Bangladesh Flag সহজেই লিখতে পারবে।

---

# 37. Viva Questions

### Q1. Bangladesh Flag আঁকতে কোন কোন shape ব্যবহার করেছি?

**Answer:** একটি Rectangle এবং একটি Circle।

---

### Q2. Green Background-এর জন্য কোন primitive?

**Answer:** `GL_QUADS`।

---

### Q3. Red Circle-এর জন্য কোন primitive?

**Answer:** `GL_POLYGON`।

---

### Q4. Circle-এর জন্য `sin()` এবং `cos()` কেন ব্যবহার করেছি?

**Answer:** Circle-এর বিভিন্ন `(x,y)` coordinate বের করার জন্য।

---

### Q5. Circle-এর Center কত?

**Answer:**

```text
(-0.1, 0.0)
```

---

### Q6. Circle-এর Radius কত?

**Answer:**

```text
0.25
```

---

### Q7. Circle-কে Left side-এ কেন রাখা হয়েছে?

**Answer:** Center X হিসেবে `-0.1` দেওয়া হয়েছে।

---

### Q8. Circle বড় করতে কী change করবো?

**Answer:** Radius `0.25` বাড়াতে হবে।

---

### Q9. Flag-এর Green part কোন shape?

**Answer:** Rectangle।

---

### Q10. Flag-কে Composite Shape বলা যায় কেন?

**Answer:** একাধিক basic shape একসাথে ব্যবহার করে তৈরি করা হয়েছে।

---

# 38. Common Mistakes

### Mistake 1: Circle-এর center ভুল করা

```cpp
float x = -0.1 + ...
```

এখানে `-0.1` হলো **Center X**, Radius না।

---

### Mistake 2: Radius ভুলে যাওয়া

```cpp
0.25
```

হলো Radius।

```text
x = centerX + radius × cos(angle)

y = centerY + radius × sin(angle)
```

---

### Mistake 3: Green Rectangle-এর coordinate ভুল করা

Rectangle:

```text
Top Left
→ Top Right
→ Bottom Right
→ Bottom Left
```

এই order-এ দিলে সহজে ঠিক থাকবে।

---

### Mistake 4: Circle আগে আঁকা

আমরা আগে Green Rectangle এবং পরে Red Circle আঁকছি।

কারণ Red Circle-কে Green-এর উপরে দেখাতে চাই।

---


# 39. Quick Revision

```text
Bangladesh Flag
       ↓
Composite Shape
       ↓
 ┌─────────────┐
 │   Green     │ → GL_QUADS
 │      ●      │ → GL_POLYGON
 │    Red      │
 └─────────────┘
```

Circle formula:

```text
x = centerX + radius × cos(angle)

y = centerY + radius × sin(angle)
```

আমাদের:

```text
Center = (-0.1, 0.0)

Radius = 0.25
```

---