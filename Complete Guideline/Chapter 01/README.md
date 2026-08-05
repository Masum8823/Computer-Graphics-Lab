# Window Creation & Background Color

> **FreeGLUT-এর মাধ্যমে একটি Window তৈরি করা এবং তার Background Color সেট করা।**

---

## 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* FreeGLUT/OpenGL window তৈরি করা
* Window-এর size নির্ধারণ করা
* Window-এর title দেওয়া
* Background color সেট করা
* `display()` function ব্যবহার করা
* `glutMainLoop()` দিয়ে program চালু রাখা

---

## 2. Complete Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);
    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("OpenGL Lab");

    glClearColor(0.0, 0.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---
