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

# 3. `glClearColor()` কী?

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

`glClearColor()` দিয়ে OpenGL-এর **clear/background color** নির্ধারণ করা হয়।

এর syntax:

```cpp
glClearColor(R, G, B, A);
```

এখানে:

```text
R → Red
G → Green
B → Blue
A → Alpha
```

---

# 4. RGB কী?

RGB হলো:

```text
R = Red
G = Green
B = Blue
```

প্রতিটি value সাধারণত:

```text
0.0 → Minimum
1.0 → Maximum
```

অর্থাৎ:

```text
0.0 = Color নেই
1.0 = Color পুরোপুরি আছে
```

---

# 5. Basic Colors

### Red

```cpp
glClearColor(1.0, 0.0, 0.0, 1.0);
```

```text
Red   = 1
Green = 0
Blue  = 0
```

Output → **Red Background**

---

### Green

```cpp
glClearColor(0.0, 1.0, 0.0, 1.0);
```

Output → **Green Background**

---

### Blue

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

Output → **Blue Background**

---

### White

```cpp
glClearColor(1.0, 1.0, 1.0, 1.0);
```

তিনটি Color-ই maximum।

Output → **White Background**

---

### Black

```cpp
glClearColor(0.0, 0.0, 0.0, 1.0);
```

তিনটি Color-ই zero।

Output → **Black Background**

---

# 6. Color Mixing

RGB-এর মূল idea হলো তিনটি color mix করে নতুন color তৈরি করা।

### Yellow

```cpp
glClearColor(1.0, 1.0, 0.0, 1.0);
```

```text
Red   = 1
Green = 1
Blue  = 0
```

Output → **Yellow**

---

### Cyan

```cpp
glClearColor(0.0, 1.0, 1.0, 1.0);
```

Output → **Cyan**

---

### Magenta

```cpp
glClearColor(1.0, 0.0, 1.0, 1.0);
```

Output → **Magenta**

---

# 7. Color Table

| Color   | Red | Green | Blue |
| ------- | --: | ----: | ---: |
| Black   |   0 |     0 |    0 |
| Red     |   1 |     0 |    0 |
| Green   |   0 |     1 |    0 |
| Blue    |   0 |     0 |    1 |
| Yellow  |   1 |     1 |    0 |
| Cyan    |   0 |     1 |    1 |
| Magenta |   1 |     0 |    1 |
| White   |   1 |     1 |    1 |

---