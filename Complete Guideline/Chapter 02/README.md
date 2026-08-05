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

# 8. মাঝামাঝি Value দিলে কী হবে?

শুধু `0` বা `1` ব্যবহার করতেই হবে এমন না।

যেমন:

```cpp
glClearColor(0.5, 0.0, 0.0, 1.0);
```

এখানে:

```text
Red = 0.5
Green = 0
Blue = 0
```

তাই Red-এর intensity কম হবে।

আবার:

```cpp
glClearColor(0.2, 0.5, 1.0, 1.0);
```

এখানে তিনটি color-এর intensity আলাদা।

অর্থাৎ `0.0` থেকে `1.0` এর মধ্যে value পরিবর্তন করে বিভিন্ন shade তৈরি করা যায়।

---

# 9. Alpha কী?

`glClearColor()`-এর fourth value হলো Alpha।

```cpp
glClearColor(R, G, B, A);
```

এখানে:

```text
A = Alpha
```

সাধারণভাবে:

```text
1.0 → Fully Opaque
0.0 → Fully Transparent
```

Basic lab code-এ আমরা সাধারণত:

```cpp
A = 1.0
```

ব্যবহার করবো।

তাই:

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এখানে:

```text
R = 0
G = 0
B = 1
A = 1
```

---

# 10. `glClearColor()` একা কি Background দেখাবে?

না।

এই দুইটা line-এর কাজ আলাদা:

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এটি Color **set** করে।

আর:

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

এটি Color Buffer **clear** করে এবং সেট করা clear color ব্যবহার করে।

তাই সাধারণত:

```cpp
glClearColor(...);

glClear(GL_COLOR_BUFFER_BIT);
```

দুটো একসাথে থাকে।

### সহজভাবে:

```text
glClearColor()
      ↓
কোন Color ব্যবহার হবে?
      ↓
glClear()
      ↓
সেই Color দিয়ে Color Buffer clear
```

---

# 11. Color Change করার নিয়ম

ধরো বর্তমানে:

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এটা Blue।

Background Green করতে শুধু:

```cpp
glClearColor(0.0, 1.0, 0.0, 1.0);
```

করলেই হবে।

Background Red করতে:

```cpp
glClearColor(1.0, 0.0, 0.0, 1.0);
```

---

# 12. Important Difference: `glClearColor()` vs `glColor3f()`

এই দুটোকে গুলিয়ে ফেলবে না।

### `glClearColor()`

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

👉 Window-এর **Background/Clear Color** সেট করে।

### `glColor3f()`

```cpp
glColor3f(1.0, 0.0, 0.0);
```

👉 Drawing করা **Object-এর Color** সেট করে।

যেমন:

```cpp
glClearColor(0.0, 0.0, 0.0, 1.0);  // Background Black

glColor3f(1.0, 0.0, 0.0);           // Object Red
```

Output:

```text
+---------------------------+
|                           |
|           RED             |
|          OBJECT           |
|                           |
|     BLACK BACKGROUND      |
|                           |
+---------------------------+
```

---

# 13. Common Mistake

অনেকে শুধু:

```cpp
glClearColor(1.0, 0.0, 0.0, 1.0);
```

লিখে ভাবে Background Red হয়ে যাবে।

কিন্তু `display()`-এ:

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

থাকতে হবে।

সঠিকভাবে:

```cpp
void display()
{
    glClear(GL_COLOR_BUFFER_BIT);
    glFlush();
}
```

---
