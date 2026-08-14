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
# 3. Line-by-Line Explanation

## `glPointSize(10);`

```cpp
glPointSize(10);
```

Point-এর **size** নির্ধারণ করে।

এখানে:

```text
Point Size = 10
```

অর্থাৎ Point সাধারণের চেয়ে বড় দেখা যাবে।

### Size পরিবর্তন করা যায়

```cpp
glPointSize(5);
```

→ ছোট Point

```cpp
glPointSize(10);
```

→ বড় Point

```cpp
glPointSize(20);
```

→ আরও বড় Point

### মনে রাখো

> `glPointSize()` → Point কত বড় হবে।

---

# 4. `glBegin(GL_POINTS);`

```cpp
glBegin(GL_POINTS);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Point আঁকবো**।

`GL_POINTS` হলো একটি OpenGL primitive.

### সহজভাবে

```text
GL_POINTS
    ↓
Point Drawing Mode
```

---

# 5. `glVertex2f(0.0, 0.0);`

```cpp
glVertex2f(0.0, 0.0);
```

এখানে Point-এর coordinate দেওয়া হয়েছে।

```text
x = 0.0
y = 0.0
```

`(0,0)` হলো screen-এর **Center**।

তাই Point টি Window-এর মাঝখানে দেখা যাবে।

```text
             +Y
              ↑
              |
              |
              ●  (0,0)
              |
              |
              ↓
             -Y
```

---

# 6. `glEnd();`

```cpp
glEnd();
```

Point drawing শেষ করে।

```text
glBegin()
    ↓
Point
    ↓
glEnd()
```

---

# 7. `glFlush();`

```cpp
glFlush();
```

OpenGL-এর drawing command execute/finish করে output দেখাতে সাহায্য করে।

সহজভাবে:

> Drawing-এর কাজ screen-এ পাঠিয়ে দাও।

---

# 8. Coordinate Change করলে কী হবে?

আমাদের code:

```cpp
glVertex2f(0.0, 0.0);
```

এতে Point Center-এ।

কিন্তু:

```cpp
glVertex2f(0.5, 0.5);
```

দিলে Point হবে:

> **Top Right**

কারণ:

```text
x = +0.5 → Right

y = +0.5 → Up
```

---

### Top Left

```cpp
glVertex2f(-0.5, 0.5);
```

```text
x = - → Left
y = + → Up
```

→ **Top Left**

---

### Bottom Left

```cpp
glVertex2f(-0.5, -0.5);
```

```text
x = - → Left
y = - → Down
```

→ **Bottom Left**

---

### Bottom Right

```cpp
glVertex2f(0.5, -0.5);
```

```text
x = + → Right
y = - → Down
```

→ **Bottom Right**

---

# 9. Coordinate Diagram

```text
                     +Y
                      ↑
                      |
          ●           |           ●
       (-0.5,0.5)     |        (0.5,0.5)
                      |
                      |
     -X ←-------------●-------------→ +X
                    (0,0)
                      |
                      |
          ●           |           ●
      (-0.5,-0.5)     |       (0.5,-0.5)
                      |
                      ↓
                     -Y
```

---

# 10. একসাথে Multiple Point

একই `glBegin(GL_POINTS)` এর মধ্যে একাধিক Point দেওয়া যায়।

```cpp
glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);
glVertex2f(0.5, 0.5);
glVertex2f(-0.5, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এখানে মোট:

```text
5টি Point
```

আঁকা হবে।

---

# 11. Point-এর Color

Point-এর color পরিবর্তন করতে `glColor3f()` ব্যবহার করা যায়।

```cpp
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);

glEnd();
```

এখানে:

```text
R = 1
G = 0
B = 0
```

তাই Point হবে **Red**।

---

# 12. Point + Size + Color

একটা complete example:

```cpp
glPointSize(15);

glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);

glEnd();
```

এখানে:

```text
glPointSize()
    ↓
Point-এর Size

glColor3f()
    ↓
Point-এর Color

glVertex2f()
    ↓
Point-এর Position
```

---

# 13. Point-এর Basic Flow

```text
glPointSize()
      ↓
Size ঠিক করে

glColor3f()
      ↓
Color ঠিক করে

glBegin(GL_POINTS)
      ↓
Point Drawing শুরু

glVertex2f(x,y)
      ↓
Point-এর Position

glEnd()
      ↓
Drawing শেষ

glFlush()
      ↓
Output Show
```

---

# 14. `glVertex2f()` আবার মনে রাখি

```cpp
glVertex2f(x, y);
```

এখানে:

```text
First value  → X → Left / Right

Second value → Y → Up / Down
```

Example:

```cpp
glVertex2f(-0.5, 0.5);
```

মানে:

```text
-0.5 → Left
+0.5 → Up
```

অর্থাৎ:

> **Top Left**

---

# 15. Important Difference

### `glPointSize()`

Point-এর **Size**

### `glColor3f()`

Point-এর **Color**

### `glVertex2f()`

Point-এর **Position**

### `GL_POINTS`

Point drawing-এর **Mode**

এগুলো খুব সহজে মনে রাখো:

```text
GL_POINTS       → কী আঁকবো?
glPointSize()   → কত বড়?
glColor3f()     → কোন Color?
glVertex2f()    → কোথায়?
```

---


# 16. Viva Questions

### Q1. Point আঁকার জন্য কোন primitive ব্যবহার করা হয়?

**Answer:** `GL_POINTS`

---

### Q2. Point-এর size কীভাবে পরিবর্তন করা হয়?

**Answer:** `glPointSize()` ব্যবহার করে।

---

### Q3. `glVertex2f()` কী কাজ করে?

**Answer:** Point-এর 2D coordinate নির্ধারণ করে।

---

### Q4. `glVertex2f(0,0)` কোথায় Point তৈরি করে?

**Answer:** Center/Origin-এ।

---

### Q5. `glVertex2f(0.5,0.5)` কোথায় Point তৈরি করবে?

**Answer:** Top Right।

---

### Q6. `glVertex2f(-0.5,0.5)` কোথায় Point তৈরি করবে?

**Answer:** Top Left।

---

### Q7. Point-এর color কীভাবে পরিবর্তন করবো?

**Answer:** `glColor3f()` ব্যবহার করে।

---

### Q8. `GL_POINTS` কী?

**Answer:** OpenGL-এর একটি primitive mode, যা Point আঁকার জন্য ব্যবহৃত হয়।

---

# 17. Common Mistakes

### Mistake 1

```cpp
glBegin(GL_POINT);
```

ভুল।

সঠিক:

```cpp
glBegin(GL_POINTS);
```

---

### Mistake 2

`glVertex2f()`-এর coordinate ভুল দেওয়া।

মনে রাখবে:

```cpp
glVertex2f(x, y);
```

---

### Mistake 3

`glPointSize()`-কে `glBegin()`-এর ভিতরে দেওয়া।

Basic code-এ এভাবে রাখবে:

```cpp
glPointSize(10);

glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);

glEnd();
```

---
