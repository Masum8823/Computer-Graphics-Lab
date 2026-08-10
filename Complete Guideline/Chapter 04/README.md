# Important FreeGLUT & OpenGL Functions

> এই file-এ Computer Graphics Lab-এর basic code-এ বারবার ব্যবহৃত গুরুত্বপূর্ণ FreeGLUT/OpenGL functions সহজ Bangla-তে দেওয়া হলো।

---

# 1. `#include <GL/glut.h>`

```cpp
#include <GL/glut.h>
```

### কাজ

OpenGL এবং FreeGLUT-এর প্রয়োজনীয় library include করে।

এটা না দিলে আমরা সাধারণত নিচের functionগুলো ব্যবহার করতে পারব না:

```text
glBegin()
glEnd()
glVertex2f()
glColor3f()
glClear()
glFlush()

glutInit()
glutCreateWindow()
glutMainLoop()
```

### সহজভাবে

> **Library include করার জন্য ব্যবহার করি।**

---
