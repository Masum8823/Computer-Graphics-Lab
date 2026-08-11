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

# 2. `glutInit()`

```cpp
glutInit(&argc, argv);
```

### কাজ

FreeGLUT initialize করে।

অর্থাৎ program-এর জন্য GLUT environment প্রস্তুত করে।

### সহজভাবে

> **FreeGLUT চালু করে।**

### সাধারণত কোথায় থাকবে?

`main()`-এর শুরুতে।

```cpp
int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    // Other code
}
```

---
# 3. `glutInitWindowSize()`

```cpp
glutInitWindowSize(800, 600);
```

### কাজ

Window-এর Width এবং Height নির্ধারণ করে।

```text
800 → Width
600 → Height
```

### Syntax

```cpp
glutInitWindowSize(width, height);
```

### Example

```cpp
glutInitWindowSize(800, 600);
```

অর্থাৎ:

> Window-এর Width = 800 pixels এবং Height = 600 pixels।

---

# 4. `glutCreateWindow()`

```cpp
glutCreateWindow("OpenGL Lab");
```

### কাজ

একটি OpenGL Window তৈরি করে।

এখানে:

```text
"OpenGL Lab"
```

হলো Window-এর Title।

### Example

```cpp
glutCreateWindow("Computer Graphics");
```

তাহলে Window-এর উপরে title হবে:

```text
Computer Graphics
```

### সহজভাবে

> **Window তৈরি করে এবং title দেয়।**

---
