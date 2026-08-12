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

# 5. `glClearColor()`

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

### কাজ

Window-এর **Background/Clear Color** নির্ধারণ করে।

### Syntax

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

### Example

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এখানে:

```text
R = 0
G = 0
B = 1
```

তাই Background হবে **Blue**।

### Common Colors

```text
Red     → (1,0,0,1)
Green   → (0,1,0,1)
Blue    → (0,0,1,1)
White   → (1,1,1,1)
Black   → (0,0,0,1)
Yellow  → (1,1,0,1)
```

---

# 6. `glClear()`

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

### কাজ

Color Buffer clear করে।

আমরা সাধারণত `glClearColor()` দিয়ে যে color set করি, `glClear()` সেই color দিয়ে buffer clear করে।

### Example

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);

glClear(GL_COLOR_BUFFER_BIT);
```

এখানে:

```text
glClearColor()
      ↓
Blue Color Set

glClear()
      ↓
Color Buffer Clear
      ↓
Blue Background
```

### সহজভাবে

> `glClearColor()` = কোন color হবে সেটা ঠিক করে।

> `glClear()` = সেই color দিয়ে screen clear করে।

---

# 7. `glFlush()`

```cpp
glFlush();
```

### কাজ

OpenGL-এর pending drawing commands execute/finish করে output দেখাতে সাহায্য করে।

### সহজভাবে

> **Drawing-এর command screen-এ পাঠিয়ে দাও।**

Basic program-এ সাধারণত:

```cpp
void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Drawing

    glFlush();
}
```

---

# 8. `glutDisplayFunc()`

```cpp
glutDisplayFunc(display);
```

### কাজ

`display()` function-কে **Display Callback Function** হিসেবে register করে।

মানে:

> Window-এ কিছু draw/display করার প্রয়োজন হলে `display()` function call করো।

### Example

```cpp
void display()
{
    glClear(GL_COLOR_BUFFER_BIT);
    glFlush();
}

int main(int argc, char** argv)
{
    // ...

    glutDisplayFunc(display);

    // ...
}
```

### খুব সহজভাবে

```text
glutDisplayFunc(display)
          ↓
"Display-এর কাজ হলে
 display() function ব্যবহার করো"
```

---

# 9. `glutMainLoop()`

```cpp
glutMainLoop();
```

### কাজ

GLUT-এর main event loop শুরু করে।

এটি Window-কে চালু রাখে এবং বিভিন্ন event handle করার জন্য অপেক্ষা করে।

যেমন:

* Window refresh
* Keyboard
* Mouse
* Window events

### সহজভাবে

> **Window চালু রাখে।**

এটা না থাকলে program তৈরি করা window-কে স্বাভাবিকভাবে event loop-এ চালিয়ে রাখবে না।

---

# 10. `glBegin()`

```cpp
glBegin(GL_LINES);
```

### কাজ

Drawing শুরু করে এবং OpenGL-কে বলে **কোন type-এর primitive আঁকবো**।

### Syntax

```cpp
glBegin(MODE);
```

### Common Modes

```text
GL_POINTS
GL_LINES
GL_TRIANGLES
GL_QUADS
GL_POLYGON
```

---

## `GL_POINTS`

```cpp
glBegin(GL_POINTS);
```

Point আঁকার জন্য।

---

## `GL_LINES`

```cpp
glBegin(GL_LINES);
```

Line আঁকার জন্য।

---

## `GL_TRIANGLES`

```cpp
glBegin(GL_TRIANGLES);
```

Triangle আঁকার জন্য।

---

## `GL_QUADS`

```cpp
glBegin(GL_QUADS);
```

চারটি Vertex দিয়ে quadrilateral আঁকার জন্য।

---

## `GL_POLYGON`

```cpp
glBegin(GL_POLYGON);
```

অনেকগুলো Vertex ব্যবহার করে closed polygon আঁকার জন্য।

---

# 11. `glVertex2f()`

```cpp
glVertex2f(0.5, 0.5);
```

### কাজ

2D coordinate নির্ধারণ করে।

### Syntax

```cpp
glVertex2f(x, y);
```

এখানে:

```text
x → Left / Right

y → Up / Down
```

### Example

```cpp
glVertex2f(0.5, 0.5);
```

Point হবে:

> **Top Right**

কারণ:

```text
x = +0.5 → Right

y = +0.5 → Up
```

### মনে রাখবে

```text
glVertex2f()
      ↓
Coordinate
```

---

# 12. `glEnd()`

```cpp
glEnd();
```

### কাজ

`glBegin()` দিয়ে শুরু করা drawing শেষ করে।

### Example

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

Flow:

```text
glBegin()
   ↓
Vertex
   ↓
Vertex
   ↓
glEnd()
```

### সহজভাবে

> `glBegin()` = Drawing Start

> `glEnd()` = Drawing Stop

---

# 13. `glPointSize()`

```cpp
glPointSize(10);
```

### কাজ

Point-এর size নির্ধারণ করে।

### Example

```cpp
glPointSize(10);

glBegin(GL_POINTS);
glVertex2f(0.0, 0.0);
glEnd();
```

এখানে Point-এর size হবে `10`।

### সহজভাবে

> **Point কত বড় হবে সেটা ঠিক করে।**

---

# 14. `glColor3f()`

```cpp
glColor3f(1.0, 0.0, 0.0);
```

### কাজ

Drawing করা object-এর color সেট করে।

### Syntax

```cpp
glColor3f(R, G, B);
```

### Example

```cpp
glColor3f(1.0, 0.0, 0.0);
```

Output → **Red**

আর:

```cpp
glColor3f(0.0, 1.0, 0.0);
```

Output → **Green**

---
# 15. `glColor3f()` vs `glClearColor()`

এটা খুব important।

### Background Color

```cpp
glClearColor(0.0, 0.0, 0.0, 1.0);
```

→ Background **Black**

### Object Color

```cpp
glColor3f(1.0, 0.0, 0.0);
```

→ Object **Red**

### সহজভাবে

```text
glClearColor()
      ↓
Background Color

glColor3f()
      ↓
Object Color
```

---