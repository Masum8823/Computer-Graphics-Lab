# Rotation

> Rotation হলো কোনো object/shape-কে একটি নির্দিষ্ট **angle** অনুযায়ী ঘুরানো।

---

# 1. Rotation কী?

সহজ ভাষায়:

```text
Object
   ↓
ঘুরবে
   ↓
New Angle
```

যেমন একটি square:

```text
Before:

┌────┐
│    │
└────┘


After Rotation:

  ╲
   ╲
    ╲
```

Shape-এর **size একই থাকবে**, শুধু angle পরিবর্তন হবে।

---

# 2. OpenGL-এ Rotation

OpenGL-এ Rotation করার জন্য:

```cpp
glRotatef(angle, x, y, z);
```

ব্যবহার করি।

সবচেয়ে important হলো:

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

এর মানে:

```text
45° → কত degree ঘুরবে

0.0 → X-axis

0.0 → Y-axis

1.0 → Z-axis
```

2D graphics-এর জন্য সাধারণত:

```text
Z = 1
```

রাখি।

---
# 3. সহজে মনে রাখো

```text
Translation → Move

Rotation → Rotate / ঘুরানো

Scaling → Size Change
```

অর্থাৎ:

```text
T → Move
R → Rotate
S → Size
```

---


# 4. Simple Rotation Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Current transformation save
    glPushMatrix();

    // Object-কে 45 degree rotate করবে
    // Z-axis বরাবর rotate করছি
    glRotatef(45.0, 0.0, 0.0, 1.0);

    // Red Color
    glColor3f(1.0, 0.0, 0.0);

    // Rectangle draw
    glBegin(GL_QUADS);

    glVertex2f(-0.3, 0.3);
    glVertex2f(0.3, 0.3);
    glVertex2f(0.3, -0.3);
    glVertex2f(-0.3, -0.3);

    glEnd();

    // আগের transformation-এ ফিরে যাওয়া
    glPopMatrix();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Rotation");

    // Background Color
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---


# 5. সবচেয়ে Important Line

```cpp
glRotatef(45.0, 0.0, 0.0, 1.0);
```

এখানে:

```text
45.0
 ↓
Rotation Angle
```

অর্থাৎ object:

```text
45°
```

ঘুরবে।

---

# 6. `glRotatef()`-এর 4টি Parameter

Function:

```cpp
glRotatef(angle, x, y, z);
```

এখানে:

```text
1st → Angle

2nd → X-axis

3rd → Y-axis

4th → Z-axis
```

---


# 7. 2D Graphics-এ কেন Z = 1?

আমরা 2D graphics করছি।

আমাদের object থাকে:

```text
X-Y Plane
```

তাই object-কে screen-এর উপর ঘোরাতে হলে **Z-axis বরাবর rotation** করতে হয়।

তাই:

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

মনে রাখবে।

---

# 8. Diagram দিয়ে বুঝি

2D coordinate:

```text
              +Y
               ↑
               |
               |
       -X ←----+----→ +X
               |
               |
               ↓
              -Y
```

Rotation হচ্ছে:

```text
       ↗
      /
     /
    ●
     \
      \
       ↘
```

অর্থাৎ object নিজের position-এর চারপাশে ঘুরছে।

---


# 9. Positive Angle

যেমন:

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

এখানে:

```text
+45°
```

মানে সাধারণভাবে **counter-clockwise** direction-এ rotate করবে।

সহজভাবে:

```text
     ↖
      |
      |
      ●
```

---

# 10. Negative Angle

যদি লিখি:

```cpp
glRotatef(-45, 0.0, 0.0, 1.0);
```

তাহলে object বিপরীত দিকে rotate করবে।

```text
+45° → Counter-clockwise

-45° → Clockwise
```

এটা exam-এর জন্য important।

---

# 11. 90 Degree Rotation

```cpp
glRotatef(90, 0.0, 0.0, 1.0);
```

মানে:

```text
Object → 90° rotate
```

---


# 12. 180 Degree Rotation

```cpp
glRotatef(180, 0.0, 0.0, 1.0);
```

মানে:

```text
Object → 180° rotate
```

---


# 13. 270 Degree Rotation

```cpp
glRotatef(270, 0.0, 0.0, 1.0);
```

মানে:

```text
Object → 270° rotate
```

---

# 14. Full Rotation

```cpp
glRotatef(360, 0.0, 0.0, 1.0);
```

360° মানে পুরো একবার ঘুরে আবার আগের অবস্থায় ফিরে আসবে।

```text
360°
 ↓
Full Circle
```

---

# 15. Rotation করলে কী Change হয়?

Rotation করলে:

```text
Position → সাধারণত same
Size     → same
Shape    → same
Angle    → Change
```

সবচেয়ে সহজ:

> **Rotation = Angle Change**

---


# 16. Translation বনাম Rotation

| Transformation | কী Change করে? |
| -------------- | -------------- |
| Translation    | Position       |
| Rotation       | Angle          |
| Scaling        | Size           |

মনে রাখো:

```text
Translation → Move
Rotation    → Turn
Scaling     → Bigger/Smaller
```

---

# 17. Rotation-এর আগে ও পরে

ধরি:

```text
Before:

┌────┐
│    │
└────┘
```

45° Rotation-এর পরে:

```text
   ╱──╲
  ╱    ╲
  ╲    ╱
   ╲──╱
```

Rectangle/square-এর size একই থাকবে।

শুধু angle change হবে।

---

# 18. `glPushMatrix()` কেন?

আমরা লিখেছি:

```cpp
glPushMatrix();

glRotatef(45, 0.0, 0.0, 1.0);

// Draw Object

glPopMatrix();
```

`glPushMatrix()`:

> বর্তমান transformation state save করে।

`glPopMatrix()`:

> আগের state-এ ফিরে যায়।

---


# 19. Push/Pop Flow

```text
glPushMatrix()
       ↓
Save Current State
       ↓
glRotatef()
       ↓
Draw Object
       ↓
glPopMatrix()
       ↓
Restore Previous State
```

---


# 20. Multiple Object-এর ক্ষেত্রে

ধরি আমাদের দুইটা object আছে।

প্রথমটা:

```text
45° rotate
```

দ্বিতীয়টা:

```text
90° rotate
```

তাহলে:

```cpp
// Object 1
glPushMatrix();

glRotatef(45, 0.0, 0.0, 1.0);

// Draw Object 1

glPopMatrix();


// Object 2
glPushMatrix();

glRotatef(90, 0.0, 0.0, 1.0);

// Draw Object 2

glPopMatrix();
```

এভাবে দুই object-এর rotation আলাদা থাকবে।

---

# 21. কেন Push/Pop দরকার?

ধরি:

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

করার পর Object 1 draw করলাম।

তারপর Object 2 draw করলাম।

Object 2-ও আগের rotation-এর effect পেতে পারে।

তাই:

```text
Push
 ↓
Rotate
 ↓
Draw
 ↓
Pop
```

ব্যবহার করলে transformation আলাদা রাখা যায়।

---

# 22. Rotation-এর Formula

Mathematicalভাবে rotation-এর ক্ষেত্রে:

```text
x' = x cosθ - y sinθ

y' = x sinθ + y cosθ
```

এখানে:

```text
θ = Rotation Angle
```

যেমন:

```text
θ = 45°
```

তাহলে point-এর নতুন coordinate বের করা যায়।

তবে OpenGL lab-এর basic code-এ সাধারণত manually এই formula লিখতে হয় না।

OpenGL:

```cpp
glRotatef()
```

দিয়ে কাজটা করে দেয়।

---


# 23. খুব সহজ Example

ধরি:

```text
Point = (1,0)
```

এখন 90° rotate করলাম।

তাহলে point:

```text
(1,0)
  ↓
(0,1)
```

অর্থাৎ:

```text
Right side
   ↓
Up side
```

চলে যাবে।

---

# 24. Rotation Direction

মনে রাখবে:

```text
+ Angle → Counter-clockwise

- Angle → Clockwise
```

যেমন:

```cpp
glRotatef(45, 0, 0, 1);
```

→ Counter-clockwise

আর:

```cpp
glRotatef(-45, 0, 0, 1);
```

→ Clockwise

---
