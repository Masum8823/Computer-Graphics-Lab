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
