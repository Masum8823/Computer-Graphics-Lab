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