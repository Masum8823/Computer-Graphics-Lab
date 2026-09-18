# DDA Line Drawing Algorithm

> **DDA = Digital Differential Analyzer**

DDA হলো computer graphics-এ **দুটি point-এর মধ্যে একটি straight line draw করার algorithm**।

---

# 1. DDA কী করে?

ধরি আমাদের দুইটা point আছে:

```text
Start Point → (x1, y1)

End Point   → (x2, y2)
```

DDA algorithm এই দুই point-এর মাঝখানে ছোট ছোট step নিয়ে:

```text
Point → Point → Point → Point → Point
```

draw করে।

এই অনেকগুলো ছোট ছোট point একসাথে দেখলে আমাদের কাছে একটা **straight line** মনে হয়।

---
# 2. Example

ধরি:

```text
Start = (2,2)

End = (8,5)
```

DDA:

```text
(2,2)
   ↓
(3,2.5)
   ↓
(4,3)
   ↓
(5,3.5)
   ↓
...
   ↓
(8,5)
```

এই pointগুলোকে plot করলে line তৈরি হবে।

---

# 3. DDA-এর Main Formula

প্রথমে:

```text
dx = x2 - x1

dy = y2 - y1
```

তারপর:

```text
steps = max(|dx|, |dy|)
```

তারপর:

```text
xIncrement = dx / steps

yIncrement = dy / steps
```

তারপর:

```text
x = x1
y = y1
```

প্রতিবার:

```text
x = x + xIncrement

y = y + yIncrement
```

এবং point plot করি।

---

# 4. Full DDA Code

```cpp
#include <GL/glut.h>
#include <math.h>

// DDA Line Drawing Function
void DrawLine(int x1, int y1, int x2, int y2)
{
    // X direction-এ কত দূরত্ব
    int dx = x2 - x1;

    // Y direction-এ কত দূরত্ব
    int dy = y2 - y1;

    // dx এবং dy-এর মধ্যে বড় মানটি steps হবে
    int steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);

    // প্রতি step-এ X কত করে বাড়বে
    float xIncrement = dx / (float)steps;

    // প্রতি step-এ Y কত করে বাড়বে
    float yIncrement = dy / (float)steps;

    // Starting point
    float x = x1;
    float y = y1;

    // Point drawing শুরু
    glBegin(GL_POINTS);

    // মোট steps বার loop চলবে
    for(int i = 0; i <= steps; i++)
    {
        // Current point draw করবে
        glVertex2f(x, y);

        // পরবর্তী point-এর জন্য X update
        x = x + xIncrement;

        // পরবর্তী point-এর জন্য Y update
        y = y + yIncrement;
    }

    // Point drawing শেষ
    glEnd();
}
```

---
# 5. Code Line by Line

এখন একদম line by line বুঝি।

---

## Step 1: Header File

```cpp
#include <GL/glut.h>
```

এটা FreeGLUT/OpenGL-এর function ব্যবহার করার জন্য।

যেমন:

```cpp
glBegin()
glEnd()
glVertex2f()
```

ইত্যাদি।

---

## Step 2: Math Header

```cpp
#include <math.h>
```

এটা mathematical function-এর জন্য।

DDA-তে আমরা:

```cpp
abs()
```

ব্যবহার করছি।

তাই `math.h` লাগছে।

---
# 6. Function তৈরি

```cpp
void DrawLine(int x1, int y1, int x2, int y2)
```

এটা আমাদের নিজের তৈরি function।

চারটা parameter:

```text
x1 → Starting X

y1 → Starting Y

x2 → Ending X

y2 → Ending Y
```

অর্থাৎ:

```text
(x1,y1) → Start

(x2,y2) → End
```

---
# 7. `dx`

```cpp
int dx = x2 - x1;
```

এটা X-axis বরাবর distance বের করে।

Formula:

```text
dx = x2 - x1
```

যেমন:

```text
x1 = 2
x2 = 8

dx = 8 - 2
   = 6
```

অর্থাৎ X direction-এ distance = `6`।

---

# 8. `dy`

```cpp
int dy = y2 - y1;
```

এটা Y-axis বরাবর distance বের করে।

Formula:

```text
dy = y2 - y1
```

যেমন:

```text
y1 = 2
y2 = 5

dy = 5 - 2
   = 3
```

অর্থাৎ Y direction-এ distance = `3`।

---
# 9. `steps`

সবচেয়ে important line:

```cpp
int steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);
```

এর মানে:

```text
steps = max(|dx|, |dy|)
```

অর্থাৎ `dx` এবং `dy`-এর মধ্যে যেটা বড়, সেটাই `steps`।

---

# 10. কেন বড় value নিতে হবে?

ধরি:

```text
dx = 6
dy = 3
```

এখানে:

```text
X distance = 6
Y distance = 3
```

তাহলে:

```text
steps = 6
```

কারণ X direction-এ বেশি distance cover করতে হবে।

এতে line-এর points যথেষ্ট smooth হবে।

---

# 11. `abs()` কী?

```cpp
abs(dx)
```

মানে:

> `dx`-এর absolute value।

যেমন:

```text
abs(5)  = 5

abs(-5) = 5
```

তাই negative distance হলেও আমরা positive step count পাই।

---


# 12. `?:` এইটা কী?

এই line:

```cpp
int steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);
```

একটু confusing হতে পারে।

এটা সহজভাবে:

```cpp
if(abs(dx) > abs(dy))
    steps = abs(dx);
else
    steps = abs(dy);
```

এর মতো।

অর্থাৎ:

```text
dx বড় → dx নাও

dy বড় → dy নাও
```

---

# 13. X Increment

```cpp
float xIncrement = dx / (float)steps;
```

এর মানে:

> প্রতিটি step-এ X কত করে change করবে।

Formula:

```text
xIncrement = dx / steps
```

---
# 14. Example

ধরি:

```text
dx = 6
steps = 6
```

তাহলে:

```text
xIncrement = 6 / 6
           = 1
```

অর্থাৎ প্রতিবার X:

```text
+1
```

করে বাড়বে।

---
# 15. কেন `(float)`?

```cpp
dx / (float)steps
```

এখানে `(float)` দেওয়ার কারণ হলো আমরা **decimal value** পেতে চাই।

যেমন:

```text
dx = 5
steps = 8
```

তাহলে:

```text
5 / 8 = 0.625
```

এই decimal value দরকার।

---

# 16. Y Increment

```cpp
float yIncrement = dy / (float)steps;
```

এর মানে:

> প্রতিটি step-এ Y কত করে change করবে।

Formula:

```text
yIncrement = dy / steps
```

---
# 17. Example

ধরি:

```text
dy = 3
steps = 6
```

তাহলে:

```text
yIncrement = 3 / 6
           = 0.5
```

অর্থাৎ প্রতিবার Y:

```text
+0.5
```

করে বাড়বে।

---

# 18. Starting Point

```cpp
float x = x1;
float y = y1;
```

এখানে আমরা শুরু করছি:

```text
x = x1

y = y1
```

অর্থাৎ:

```text
(x,y) = Starting Point
```

---

# 19. `glBegin(GL_POINTS)`

```cpp
glBegin(GL_POINTS);
```

আমরা DDA-তে অনেকগুলো point plot করব।

তাই:

```text
GL_POINTS
```

ব্যবহার করছি।

---
# 20. Loop

```cpp
for(int i = 0; i <= steps; i++)
```

এই loop:

```text
0 → 1 → 2 → 3 → ... → steps
```

পর্যন্ত চলবে।

প্রতিটি iteration-এ একটি point draw হবে।

---

# 21. Point Draw

```cpp
glVertex2f(x, y);
```

এটা current `(x,y)` point screen-এ draw করবে।

যেমন:

```text
(2,2)
```

তারপর:

```text
(3,2.5)
```

তারপর:

```text
(4,3)
```

ইত্যাদি।

---

# 22. X Update

```cpp
x = x + xIncrement;
```

মানে:

```text
নতুন X = পুরোনো X + X Increment
```

যেমন:

```text
x = 2
xIncrement = 1

new x = 2 + 1
      = 3
```

---

# 23. Y Update

```cpp
y = y + yIncrement;
```

মানে:

```text
নতুন Y = পুরোনো Y + Y Increment
```

যেমন:

```text
y = 2
yIncrement = 0.5

new y = 2 + 0.5
      = 2.5
```

---

# 24. `glEnd()`

```cpp
glEnd();
```

Point drawing শেষ।

---
# 25. পুরো Process একসাথে

ধরি:

```text
Start = (2,2)

End = (8,5)
```

তাহলে:

```text
dx = 8 - 2 = 6

dy = 5 - 2 = 3

steps = max(6,3)
      = 6
```

তারপর:

```text
xIncrement = 6/6
           = 1

yIncrement = 3/6
           = 0.5
```

Start:

```text
x = 2
y = 2
```

---

# 26. Iteration Table

এখন প্রতি step-এ কী হচ্ছে দেখি:

| Step |   X |   Y |
| ---: | --: | --: |
|    0 | 2.0 | 2.0 |
|    1 | 3.0 | 2.5 |
|    2 | 4.0 | 3.0 |
|    3 | 5.0 | 3.5 |
|    4 | 6.0 | 4.0 |
|    5 | 7.0 | 4.5 |
|    6 | 8.0 | 5.0 |

এই pointগুলো plot করলে line তৈরি হবে।

---
# 27. Visual Idea

```text
Y
↑
5 |                 ●
4 |             ●
3 |         ●
2 |     ●
1 |
  +------------------------→ X
      2   3   4   5   6   7   8
```

অনেকগুলো point:

```text
●
  ●
    ●
      ●
        ●
```

একসাথে দেখলে straight line।

---

# 28. Full OpenGL Program

এখন DDA-কে complete FreeGLUT program-এর মধ্যে বসাই।

```cpp
#include <GL/glut.h>
#include <math.h>

// DDA Algorithm
void DrawLine(int x1, int y1, int x2, int y2)
{
    // X এবং Y distance
    int dx = x2 - x1;
    int dy = y2 - y1;

    // বড় distance-টাই steps
    int steps = abs(dx) > abs(dy) ? abs(dx) : abs(dy);

    // প্রতি step-এ X কত change করবে
    float xIncrement = dx / (float)steps;

    // প্রতি step-এ Y কত change করবে
    float yIncrement = dy / (float)steps;

    // Starting point
    float x = x1;
    float y = y1;

    // Point drawing শুরু
    glBegin(GL_POINTS);

    // প্রতিটি point draw
    for(int i = 0; i <= steps; i++)
    {
        glVertex2f(x, y);

        // পরের point
        x = x + xIncrement;
        y = y + yIncrement;
    }

    // Point drawing শেষ
    glEnd();
}

void display()
{
    // Screen clear
    glClear(GL_COLOR_BUFFER_BIT);

    // Line draw
    DrawLine(-200, -100, 200, 150);

    // Drawing শেষ
    glFlush();
}

int main(int argc, char** argv)
{
    // GLUT initialize
    glutInit(&argc, argv);

    // Window size
    glutInitWindowSize(800, 600);

    // Window create
    glutCreateWindow("DDA Line");

    // Background color
    glClearColor(1.0, 1.0, 1.0, 1.0);

    // Display function
    glutDisplayFunc(display);

    // Main loop
    glutMainLoop();

    return 0;
}
```

---

