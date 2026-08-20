# Draw a Rectangle

> OpenGL-এ ৪টি Vertex ব্যবহার করে একটি Rectangle আঁকার basic method।

---

# 1. কী শিখবো?

এই file থেকে আমরা শিখবো:

* `GL_QUADS` কী
* Rectangle-এর জন্য কয়টি Vertex লাগে
* ৪টি coordinate কীভাবে Rectangle তৈরি করে
* Vertex-এর order কেন important
* Rectangle-এর position ও size কীভাবে change করতে হয়
* Rectangle-এর color কীভাবে দিতে হয়

---
# 2. Basic Rectangle Code

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

এখানে মোট **৪টি Vertex** আছে।

```text
4 Vertex → 1 Rectangle
```

---

# 3. `glBegin(GL_QUADS)`

```cpp
glBegin(GL_QUADS);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Quadrilateral/Quad** আঁকবো।

`GL_QUADS`-এ সাধারণভাবে **৪টি Vertex** মিলে একটি four-sided shape তৈরি করে।

```text
GL_QUADS
   ↓
4 Vertex
   ↓
1 Quad
```

আমাদের Rectangle হলো একটি Quad।

---

# 4. প্রথম Vertex

```cpp
glVertex2f(-0.5, 0.5);
```

Coordinate:

```text
x = -0.5 → Left
y =  0.5 → Up
```

তাই এটি:

> **Top Left**

```text
● (-0.5,0.5)
```

---

# 5. দ্বিতীয় Vertex

```cpp
glVertex2f(0.5, 0.5);
```

এখানে:

```text
x = 0.5 → Right
y = 0.5 → Up
```

তাই এটি:

> **Top Right**

```text
(-0.5,0.5) ●────────● (0.5,0.5)
```

---

# 6. তৃতীয় Vertex

```cpp
glVertex2f(0.5, -0.5);
```

এখানে:

```text
x = 0.5 → Right
y = -0.5 → Down
```

তাই এটি:

> **Bottom Right**

```text
(-0.5,0.5) ●────────● (0.5,0.5)
                         |
                         |
                         ● (0.5,-0.5)
```

---

# 7. চতুর্থ Vertex

```cpp
glVertex2f(-0.5, -0.5);
```

এখানে:

```text
x = -0.5 → Left
y = -0.5 → Down
```

তাই এটি:

> **Bottom Left**

শেষে পুরো shape হবে:

```text
        (-0.5,0.5) ●────────────● (0.5,0.5)
                   |              |
                   |              |
                   |              |
        (-0.5,-0.5)●────────────● (0.5,-0.5)
```

---

# 8. চারটি Vertex কীভাবে Rectangle হলো?

আমাদের চারটি Vertex:

```text
1 → (-0.5,  0.5)  Top Left

2 → ( 0.5,  0.5)  Top Right

3 → ( 0.5, -0.5)  Bottom Right

4 → (-0.5, -0.5)  Bottom Left
```

OpenGL এগুলোকে order অনুযায়ী connect করে:

```text
1 → 2
2 → 3
3 → 4
4 → 1
```

তাই Rectangle তৈরি হয়।

---

# 9. Vertex Order খুব Important

আমাদের code:

```cpp
glVertex2f(-0.5, 0.5);   // 1
glVertex2f(0.5, 0.5);    // 2
glVertex2f(0.5, -0.5);   // 3
glVertex2f(-0.5, -0.5);  // 4
```

এটা basically:

```text
1 → 2 → 3 → 4 → 1
```

অর্থাৎ এক পাশ থেকে শুরু করে চারপাশ ঘুরে আসছি।

### সহজভাবে মনে রাখো

> **Top Left → Top Right → Bottom Right → Bottom Left**

এটা Rectangle-এর জন্য খুব easy sequence।

---

# 10. কেন সরাসরি ১ থেকে ৩ এ যাওয়া যাবে না?

Rectangle-এর চারপাশ follow করতে হবে।

সঠিক:

```text
1 → 2 → 3 → 4 → 1
```

ভুলভাবে:

```text
1 → 3 → 2 → 4
```

দিলে shape-এর vertex order এলোমেলো হয়ে যেতে পারে।

তাই basic lab-এর জন্য সবসময় চারপাশ ঘুরে coordinate দাও।

---

# 11. Rectangle-এর Color

Rectangle-এর color দিতে:

```cpp
glColor3f(1.0, 0.0, 0.0);
```

তারপর:

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

এখানে Rectangle হবে **Red**।

---

# 12. Complete Colored Rectangle

```cpp
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

Flow:

```text
glColor3f()
     ↓
Rectangle-এর Color

glBegin(GL_QUADS)
     ↓
Quad Mode

4 × glVertex2f()
     ↓
4 Corner

glEnd()
     ↓
Drawing শেষ
```

---

# 13. Rectangle-এর Size কীভাবে Change করবো?

বর্তমানে:

```cpp
glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);
```

এটা relatively বড় Rectangle।

ছোট করতে পারি:

```cpp
glVertex2f(-0.2, 0.2);
glVertex2f(0.2, 0.2);
glVertex2f(0.2, -0.2);
glVertex2f(-0.2, -0.2);
```

কারণ coordinate values ছোট হয়েছে।

```text
Coordinate values ছোট
        ↓
Corners কাছাকাছি
        ↓
Rectangle ছোট
```

---

# 14. Rectangle-এর Width বাড়ানো

যদি চাই Rectangle বেশি wide হবে:

```cpp
glVertex2f(-0.8, 0.4);
glVertex2f(0.8, 0.4);
glVertex2f(0.8, -0.4);
glVertex2f(-0.8, -0.4);
```

এখানে:

```text
X → ±0.8
Y → ±0.4
```

তাই:

> Width বেশি, Height কম।

```text
      ●────────────────────●
      |                    |
      |                    |
      ●────────────────────●
```

---

# 15. Rectangle-এর Height বাড়ানো

```cpp
glVertex2f(-0.4, 0.8);
glVertex2f(0.4, 0.8);
glVertex2f(0.4, -0.8);
glVertex2f(-0.4, -0.8);
```

এখানে:

```text
X → ±0.4
Y → ±0.8
```

তাই:

> Height বেশি, Width কম।

---

# 16. Rectangle-এর Position Change

ধরো Rectangle-টা Center-এ না থেকে Right Side-এ চাই।

```cpp
glVertex2f(0.2, 0.5);
glVertex2f(0.8, 0.5);
glVertex2f(0.8, -0.5);
glVertex2f(0.2, -0.5);
```

সব X positive হওয়ায় Rectangle ডানদিকে চলে যাবে।

```text
              Rectangle
                  ↓
              ┌────────┐
              │        │
              │        │
              └────────┘
```

---

# 17. Coordinate দিয়ে Rectangle চিনে রাখো

এই চারটা coordinate খুব important:

```text
(-0.5,  0.5) → Top Left
( 0.5,  0.5) → Top Right
( 0.5, -0.5) → Bottom Right
(-0.5, -0.5) → Bottom Left
```

Diagram:

```text
             +Y
              ↑

     TL ●────────────● TR
        |             |
        |             |
        |             |
     BL ●────────────● BR

              → +X
```

---

# 18. Rectangle-এর Basic Structure

Exam-এ Rectangle আঁকতে এই structure মনে রাখলেই হবে:

```cpp
glBegin(GL_QUADS);

glVertex2f(Left, Top);
glVertex2f(Right, Top);
glVertex2f(Right, Bottom);
glVertex2f(Left, Bottom);

glEnd();
```

আমাদের example:

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

---

# 19. Rectangle vs Triangle vs Line

| Shape     | OpenGL Mode    | Vertex |
| --------- | -------------- | -----: |
| Point     | `GL_POINTS`    |      1 |
| Line      | `GL_LINES`     |      2 |
| Triangle  | `GL_TRIANGLES` |      3 |
| Rectangle | `GL_QUADS`     |      4 |

সবচেয়ে সহজে:

```text
1 Vertex → Point

2 Vertex → Line

3 Vertex → Triangle

4 Vertex → Quad/Rectangle
```

---

# 20. Multiple Rectangle

`GL_QUADS` ব্যবহার করে একাধিক Quad আঁকা যায়।

Rule:

```text
4 Vertex → 1 Quad
8 Vertex → 2 Quad
12 Vertex → 3 Quad
```

Formula:

```text
Number of Quads = Number of Vertices ÷ 4
```

Example:

```cpp
glBegin(GL_QUADS);

// Rectangle 1
glVertex2f(-0.8, 0.5);
glVertex2f(-0.2, 0.5);
glVertex2f(-0.2, -0.5);
glVertex2f(-0.8, -0.5);

// Rectangle 2
glVertex2f(0.2, 0.5);
glVertex2f(0.8, 0.5);
glVertex2f(0.8, -0.5);
glVertex2f(0.2, -0.5);

glEnd();
```

এখানে:

```text
8 Vertex
   ↓
8 ÷ 4
   ↓
2 Rectangle
```

---

# 21. Complete Program

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    glColor3f(1.0, 0.0, 0.0);

    glBegin(GL_QUADS);

    glVertex2f(-0.5, 0.5);
    glVertex2f(0.5, 0.5);
    glVertex2f(0.5, -0.5);
    glVertex2f(-0.5, -0.5);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Rectangle");

    glClearColor(0.0, 0.0, 0.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 22. Code Flow

```text
glClear()
   ↓
Screen Clear

glColor3f()
   ↓
Rectangle Color

glBegin(GL_QUADS)
   ↓
Quad Mode

Vertex 1
   ↓
Top Left

Vertex 2
   ↓
Top Right

Vertex 3
   ↓
Bottom Right

Vertex 4
   ↓
Bottom Left

glEnd()
   ↓
Drawing শেষ

glFlush()
   ↓
Output
```

---


# 23. Viva Questions

### Q1. Rectangle আঁকার জন্য কোন primitive ব্যবহার করা হয়েছে?

**Answer:** `GL_QUADS`

---

### Q2. একটি Rectangle-এর জন্য কয়টি Vertex লাগে?

**Answer:** 4টি Vertex।

---

### Q3. `GL_QUADS`-এ 8টি Vertex দিলে কয়টি Quad হবে?

**Answer:** 2টি Quad।

```text
8 ÷ 4 = 2
```

---

### Q4. Rectangle-এর Top Left coordinate কোনটি?

**Answer:** `(-0.5, 0.5)`

---

### Q5. Top Right coordinate কোনটি?

**Answer:** `(0.5, 0.5)`

---

### Q6. Bottom Right coordinate কোনটি?

**Answer:** `(0.5, -0.5)`

---

### Q7. Bottom Left coordinate কোনটি?

**Answer:** `(-0.5, -0.5)`

---

### Q8. Rectangle-এর width কীভাবে বাড়াবো?

**Answer:** X coordinate-এর difference বাড়াতে হবে।

সহজভাবে:

```text
Left আরও Left
Right আরও Right
```

---

### Q9. Rectangle-এর height কীভাবে বাড়াবো?

**Answer:** Y coordinate-এর difference বাড়াতে হবে।

```text
Top আরও Up
Bottom আরও Down
```

---

### Q10. Rectangle-এর color কীভাবে পরিবর্তন করবো?

**Answer:** `glColor3f()` ব্যবহার করে।

---

# 24. Common Mistakes

### Mistake 1: `GL_QUAD` লেখা

ভুল:

```cpp
glBegin(GL_QUAD);
```

সঠিক:

```cpp
glBegin(GL_QUADS);
```

---

### Mistake 2: ৪টির কম Vertex

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5,0.5);
glVertex2f(0.5,0.5);
glVertex2f(0.5,-0.5);

glEnd();
```

এখানে মাত্র 3টি Vertex।

```text
3 Vertex → Triangle-এর জন্য ঠিক
3 Vertex → Quad-এর জন্য ঠিক না
```

Rectangle/Quad-এর জন্য 4টি Vertex লাগবে।

---

### Mistake 3: Vertex order এলোমেলো করা

Basic Rectangle-এর জন্য এই order follow করো:

```text
Top Left
    ↓
Top Right
    ↓
Bottom Right
    ↓
Bottom Left
```

অর্থাৎ:

```text
(-0.5, 0.5)
( 0.5, 0.5)
( 0.5,-0.5)
(-0.5,-0.5)
```

---

# 25. Quick Revision

```text
GL_QUADS
    ↓
Quad/Rectangle

4 Vertex
    ↓
1 Rectangle

Vertex 1
    ↓
Top Left

Vertex 2
    ↓
Top Right

Vertex 3
    ↓
Bottom Right

Vertex 4
    ↓
Bottom Left
```
