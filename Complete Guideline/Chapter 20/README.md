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