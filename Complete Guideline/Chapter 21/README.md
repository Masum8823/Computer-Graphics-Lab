# Scaling

> Scaling হলো কোনো object/shape-এর **size বড় বা ছোট করা**।

---

# 1. Scaling কী?

সহজ ভাষায়:

```text
Object
   ↓
Size Change
   ↓
Scaling
```

যেমন:

```text
Before:

  ┌───┐
  │   │
  └───┘


After Scaling:

  ┌───────┐
  │       │
  │       │
  └───────┘
```

Object-এর shape একই থাকবে, কিন্তু **size change হবে**।

---

# 2. OpenGL-এ Scaling

OpenGL-এ Scaling করার function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
Sx → X direction-এ কত গুণ বড়/ছোট হবে

Sy → Y direction-এ কত গুণ বড়/ছোট হবে

Sz → Z direction-এ কত গুণ বড়/ছোট হবে
```

2D graphics-এর ক্ষেত্রে সাধারণত:

```cpp
glScalef(Sx, Sy, 1.0);
```

ব্যবহার করি।

---
# 2. OpenGL-এ Scaling

OpenGL-এ Scaling করার function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
Sx → X direction-এ কত গুণ বড়/ছোট হবে

Sy → Y direction-এ কত গুণ বড়/ছোট হবে

Sz → Z direction-এ কত গুণ বড়/ছোট হবে
```

2D graphics-এর ক্ষেত্রে সাধারণত:

```cpp
glScalef(Sx, Sy, 1.0);
```

ব্যবহার করি।

---



# 3. সহজে মনে রাখো

Transformation তিনটা:

```text
Translation → Position Change
Rotation    → Angle Change
Scaling     → Size Change
```

অর্থাৎ:

```text
T → Move
R → Rotate
S → Size
```

---


# 4. Simple Scaling Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Current transformation save
    glPushMatrix();

    // Object-এর size 2 গুণ বড় করবে
    // X = 2, Y = 2
    glScalef(2.0, 2.0, 1.0);

    // Red Color
    glColor3f(1.0, 0.0, 0.0);

    // Rectangle draw
    glBegin(GL_QUADS);

    glVertex2f(-0.2, 0.2);
    glVertex2f(0.2, 0.2);
    glVertex2f(0.2, -0.2);
    glVertex2f(-0.2, -0.2);

    glEnd();

    // আগের transformation-এ ফিরে যাওয়া
    glPopMatrix();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Scaling");

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
glScalef(2.0, 2.0, 1.0);
```

এখানে:

```text
2.0 → X direction-এ 2 গুণ

2.0 → Y direction-এ 2 গুণ

1.0 → Z direction-এ কোনো change নেই
```

তাই object:

```text
Width  → 2 গুণ
Height → 2 গুণ
```

বড় হবে।

---


# 6. `glScalef()`-এর 3টি Parameter

Function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
1st → X-axis scaling

2nd → Y-axis scaling

3rd → Z-axis scaling
```

2D-এর জন্য:

```text
Sz = 1.0
```

রাখি।

---

# 7. Scaling Factor কী?

Scaling-এর value-কে Scaling Factor বলা যায়।

যেমন:

```cpp
glScalef(2.0, 2.0, 1.0);
```

এখানে:

```text
X factor = 2
Y factor = 2
```

মানে দুই direction-এই object 2 গুণ হবে।

---


# 8. Factor = 1 হলে কী হয়?

```cpp
glScalef(1.0, 1.0, 1.0);
```

তাহলে:

```text
X → 1 গুণ
Y → 1 গুণ
```

অর্থাৎ:

> কোনো size change হবে না।

---