# Draw a House

> OpenGL-এ basic shapes একসাথে ব্যবহার করে একটি simple House আঁকা।

---

# 1. House কীভাবে বানাবো?

একটা simple House-কে কয়েকটা অংশে ভাগ করবো:

```text
       /\
      /  \        ← Roof (Triangle)
     /____\
     |    |
     | [] |       ← Window
     |    |
     | __ |
     ||  ||       ← Door
     |____|
```

আমরা ব্যবহার করবো:

```text
House Body → GL_QUADS
Roof       → GL_TRIANGLES
Door       → GL_QUADS
Window     → GL_QUADS
```

অর্থাৎ:

```text
Basic Shapes
     ↓
Combine
     ↓
House
```

---


# 2. Basic House Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // =========================
    // House Body
    // =========================

    glColor3f(0.8, 0.5, 0.2);

    glBegin(GL_QUADS);

    glVertex2f(-0.6, 0.4);
    glVertex2f(0.6, 0.4);
    glVertex2f(0.6, -0.6);
    glVertex2f(-0.6, -0.6);

    glEnd();


    // =========================
    // Roof
    // =========================

    glColor3f(1.0, 0.0, 0.0);

    glBegin(GL_TRIANGLES);

    glVertex2f(-0.7, 0.4);
    glVertex2f(0.7, 0.4);
    glVertex2f(0.0, 0.9);

    glEnd();


    // =========================
    // Door
    // =========================

    glColor3f(0.3, 0.1, 0.0);

    glBegin(GL_QUADS);

    glVertex2f(-0.2, -0.6);
    glVertex2f(0.2, -0.6);
    glVertex2f(0.2, 0.0);
    glVertex2f(-0.2, 0.0);

    glEnd();


    // =========================
    // Window
    // =========================

    glColor3f(0.0, 0.5, 1.0);

    glBegin(GL_QUADS);

    glVertex2f(0.3, 0.2);
    glVertex2f(0.5, 0.2);
    glVertex2f(0.5, 0.0);
    glVertex2f(0.3, 0.0);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("House");

    // Background White
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---