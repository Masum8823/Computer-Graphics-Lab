# Draw a Point

> OpenGL-এ একটি নির্দিষ্ট coordinate-এ একটি Point আঁকার basic method।

---

## 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* `GL_POINTS` কী
* `glPointSize()` কী
* `glVertex2f()` দিয়ে Point-এর position দেওয়া
* Point-এর size পরিবর্তন করা
* Coordinate দেখে Point-এর location বের করা

---


# 2. Complete Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    glPointSize(10);

    glBegin(GL_POINTS);

    glVertex2f(0.0, 0.0);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Draw a Point");

    glClearColor(0.0, 0.0, 0.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---
