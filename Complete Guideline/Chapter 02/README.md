# Background Color in FreeGLUT

> **OpenGL Window-এর Background Color কীভাবে পরিবর্তন করতে হয়।**

---

## 1. কী শিখবো?

এই file-এ আমরা শিখবো:

* `glClearColor()` কী
* RGB Color কীভাবে কাজ করে
* Alpha কী
* বিভিন্ন Color সেট করা
* `glClearColor()` এবং `glClear()`-এর সম্পর্ক
* Background Color পরিবর্তন করার সহজ নিয়ম

---

# 2. Basic Code

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

    glutCreateWindow("Background Color");

    glClearColor(0.0, 0.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

এই code run করলে Window-এর Background **Blue** হবে।

---