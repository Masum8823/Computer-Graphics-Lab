# Draw a Line

> OpenGL-এ দুটি Point/Vertex-এর মধ্যে একটি straight line আঁকার basic method।

---

## 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* `GL_LINES` কী
* Line আঁকার জন্য কয়টি coordinate লাগে
* `glVertex2f()` কীভাবে Line-এর starting ও ending point দেয়
* Horizontal, Vertical ও Diagonal Line
* Line-এর color পরিবর্তন
* একাধিক Line আঁকার basic rule

---

# 2. Basic Code

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

এটাই আমাদের মূল Line drawing code।

---

# 3. Line কীভাবে তৈরি হলো?

এখানে দুইটি Vertex দেওয়া হয়েছে:

```cpp
glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);
```

প্রথম Point:

```text
(-0.5, 0.0)
```

দ্বিতীয় Point:

```text
(0.5, 0.0)
```

OpenGL এই দুইটি Point-এর মধ্যে সরাসরি একটি straight line তৈরি করে।

```text
(-0.5,0) ●──────────────● (0.5,0)
```

---

# 4. `glBegin(GL_LINES)`

```cpp
glBegin(GL_LINES);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Line আঁকবো**।

এখানে:

```text
GL_LINES
   ↓
Line Drawing Mode
```

---

# 5. `glVertex2f()` দিয়ে দুইটি Point

### First Point

```cpp
glVertex2f(-0.5, 0.0);
```

এটি Line-এর **starting point**।

```text
X = -0.5 → Left
Y =  0.0 → Center level
```

তাই Point টি Center-এর বাম দিকে।

---

### Second Point

```cpp
glVertex2f(0.5, 0.0);
```

এটি Line-এর **ending point**।

```text
X = 0.5 → Right
Y = 0.0 → Center level
```

তাই Point টি Center-এর ডান দিকে।

---

# 6. কেন দুইটি Point লাগে?

Line হলো দুইটি Point-এর মধ্যে একটি straight connection।

তাই:

```text
Point 1 ───────── Point 2
```

এর জন্য minimum দুইটি vertex লাগে।

```cpp
glVertex2f(x1, y1);
glVertex2f(x2, y2);
```

এখানে:

```text
(x1,y1) → Starting Point
(x2,y2) → Ending Point
```

---
# 7. Horizontal Line

আমাদের code:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

দুই Point-এর `Y` একই:

```text
Y = 0.0
Y = 0.0
```

তাই Line হবে **Horizontal**।

```text
        ●────────────────●
     (-0.5,0)         (0.5,0)
```

### Rule

> **Y same → Horizontal Line**

---

# 8. Vertical Line

যদি:

```cpp
glBegin(GL_LINES);

glVertex2f(0.0, -0.5);
glVertex2f(0.0, 0.5);

glEnd();
```

এখানে দুই Point-এর `X` একই:

```text
X = 0.0
X = 0.0
```

তাই Line হবে **Vertical**।

```text
          ● (0,0.5)
          |
          |
          |
          ● (0,-0.5)
```

### Rule

> **X same → Vertical Line**

---

# 9. Diagonal Line

যদি:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, -0.5);
glVertex2f(0.5, 0.5);

glEnd();
```

Coordinate:

```text
Starting Point → (-0.5,-0.5)

Ending Point   → (0.5,0.5)
```

তাই Line হবে diagonal।

```text
(0.5,0.5) ●
            \
             \
              \
               \
(-0.5,-0.5) ●
```

এখানে:

```text
X → Negative থেকে Positive

Y → Negative থেকে Positive
```

তাই Line **bottom-left থেকে top-right** গেছে।

---

# 10. উল্টো Diagonal

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এখানে:

```text
(-0.5,0.5) → Top Left

(0.5,-0.5) → Bottom Right
```

তাই:

```text
(-0.5,0.5) ●
             \
              \
               \
                \
                 ● (0.5,-0.5)
```

---


# 11. Line-এর Color

Line-এর color দিতে:

```cpp
glColor3f(1.0, 0.0, 0.0);
```

তারপর Line:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

Complete:

```cpp
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

এখানে Line হবে **Red**।

---

# 12. Line-এর Basic Structure

সবচেয়ে important structure:

```cpp
glBegin(GL_LINES);

glVertex2f(x1, y1);
glVertex2f(x2, y2);

glEnd();
```

এখানে:

```text
(x1,y1)
   ↓
Starting Point

(x2,y2)
   ↓
Ending Point
```

---

# 13. Multiple Lines

`GL_LINES` ব্যবহার করে একসাথে একাধিক Line আঁকা যায়।

কিন্তু এখানে একটি গুরুত্বপূর্ণ rule আছে:

> **প্রতি ২টি Vertex = ১টি Line**

Example:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.8, 0.0);
glVertex2f(-0.2, 0.0);

glVertex2f(0.2, 0.0);
glVertex2f(0.8, 0.0);

glEnd();
```

এখানে মোট:

```text
4 Vertices
```

তাই:

```text
4 ÷ 2 = 2 Lines
```

---

# 14. Multiple Line-এর Rule

মনে রাখবে:

```text
2 Vertex → 1 Line

4 Vertex → 2 Lines

6 Vertex → 3 Lines

8 Vertex → 4 Lines
```

Formula:

```text
Number of Lines = Number of Vertices ÷ 2
```

---

# 15. Example: দুইটি Line

```cpp
glBegin(GL_LINES);

glVertex2f(-0.8, 0.0);
glVertex2f(-0.2, 0.0);

glVertex2f(0.2, 0.0);
glVertex2f(0.8, 0.0);

glEnd();
```

OpenGL এটাকে এভাবে pair করবে:

```text
Vertex 1 + Vertex 2 → Line 1

Vertex 3 + Vertex 4 → Line 2
```

অর্থাৎ:

```text
●────────●       ●────────●
```

---

# 16. `GL_LINES`-এ Vertex Pairing

এটা খুব important।

ধরো:

```cpp
glBegin(GL_LINES);

glVertex2f(-0.8, 0.0);  // Vertex 1
glVertex2f(-0.2, 0.0);  // Vertex 2

glVertex2f(0.2, 0.0);   // Vertex 3
glVertex2f(0.8, 0.0);   // Vertex 4

glEnd();
```

OpenGL করবে:

```text
Vertex 1 + Vertex 2
        ↓
      Line 1

Vertex 3 + Vertex 4
        ↓
      Line 2
```

---

# 17. Line-এর Width

Basic line-এর width পরিবর্তন করতে:

```cpp
glLineWidth(5);
```

Example:

```cpp
glLineWidth(5);

glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

এখানে Line একটু মোটা হবে।

### মনে রাখো

```text
glPointSize() → Point-এর Size

glLineWidth() → Line-এর Width
```

---

# 18. Point vs Line

| Point           | Line                    |
| --------------- | ----------------------- |
| `GL_POINTS`     | `GL_LINES`              |
| 1 Vertex        | 2 Vertices              |
| `glPointSize()` | `glLineWidth()`         |
| একটি অবস্থান    | দুই Point-এর connection |

সহজভাবে:

```text
Point
  ↓
একটা Vertex

Line
  ↓
দুইটা Vertex
```

---

# 19. Coordinate দেখে Line চিনবো কীভাবে?

### Horizontal

```cpp
(-0.5, 0)
(0.5, 0)
```

Y same।

```text
→ Horizontal
```

---

### Vertical

```cpp
(0, -0.5)
(0, 0.5)
```

X same।

```text
→ Vertical
```

---

### Diagonal

```cpp
(-0.5,-0.5)
(0.5,0.5)
```

X এবং Y দুটোই পরিবর্তন হয়েছে।

```text
→ Diagonal
```

---

# 20. Complete Basic Program

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    glColor3f(1.0, 0.0, 0.0);

    glLineWidth(5);

    glBegin(GL_LINES);

    glVertex2f(-0.5, 0.0);
    glVertex2f(0.5, 0.0);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Draw Line");

    glClearColor(0.0, 0.0, 0.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---


# 21. Code Flow

```text
glClear()
   ↓
Background Clear

glColor3f()
   ↓
Line Color

glLineWidth()
   ↓
Line Width

glBegin(GL_LINES)
   ↓
Line Mode

glVertex2f()
   ↓
Starting Point

glVertex2f()
   ↓
Ending Point

glEnd()
   ↓
Drawing End

glFlush()
   ↓
Output
```

---

# 22. Viva Questions

### Q1. Line আঁকার জন্য কোন primitive ব্যবহার করা হয়?

**Answer:** `GL_LINES`

---

### Q2. একটি Line আঁকার জন্য কয়টি Vertex লাগে?

**Answer:** 2টি Vertex।

---

### Q3. `glVertex2f()` কী কাজ করে?

**Answer:** 2D coordinate নির্ধারণ করে।

---

### Q4. `GL_LINES`-এ 4টি Vertex দিলে কয়টি Line হবে?

**Answer:** 2টি Line।

কারণ:

```text
4 ÷ 2 = 2
```

---

### Q5. দুই Point-এর Y coordinate same হলে Line কেমন হবে?

**Answer:** Horizontal Line।

---

### Q6. দুই Point-এর X coordinate same হলে Line কেমন হবে?

**Answer:** Vertical Line।

---

### Q7. Line-এর color কীভাবে পরিবর্তন করবো?

**Answer:** `glColor3f()` ব্যবহার করে।

---

### Q8. Line-এর width কীভাবে পরিবর্তন করবো?

**Answer:** `glLineWidth()` ব্যবহার করে।

---

### Q9. `(-0.5,-0.5)` থেকে `(0.5,0.5)` Line কোন দিকে যাবে?

**Answer:** Bottom Left থেকে Top Right।

---

### Q10. `(-0.5,0.5)` থেকে `(0.5,-0.5)` Line কোন দিকে যাবে?

**Answer:** Top Left থেকে Bottom Right।

---

# 23. Quick Revision

```text
GL_LINES
   ↓
Line আঁকে

2 Vertex
   ↓
1 Line

glVertex2f()
   ↓
Starting + Ending Point

Y same
   ↓
Horizontal

X same
   ↓
Vertical

X & Y change
   ↓
Diagonal

glColor3f()
   ↓
Line Color

glLineWidth()
   ↓
Line Width
```

---

# 24. One-Line Memory Trick

> **`GL_LINES`-এ প্রতি ২টা Vertex মিলে ১টা Line তৈরি হয়।**
