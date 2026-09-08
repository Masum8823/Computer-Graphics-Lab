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

