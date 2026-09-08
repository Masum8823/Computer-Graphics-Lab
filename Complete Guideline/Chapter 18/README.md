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
