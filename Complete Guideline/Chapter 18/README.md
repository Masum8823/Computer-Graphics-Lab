# Draw a House

> OpenGL-এ basic shapes একসাথে ব্যবহার করে একটি simple House আঁকা।

---

# 1. House কীভাবে বানাবো?

একটা simple House-কে কয়েকটা অংশে ভাগ করবো:

```text
       /\
      /  \        ← Roof (Triangle)
     /____\
     |    |
     | [] |       ← Window
     |    |
     | __ |
     ||  ||       ← Door
     |____|
```

আমরা ব্যবহার করবো:

```text
House Body → GL_QUADS
Roof       → GL_TRIANGLES
Door       → GL_QUADS
Window     → GL_QUADS
```

অর্থাৎ:

```text
Basic Shapes
     ↓
Combine
     ↓
House
```

---


# 2. Basic House Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // =========================
    // House Body
    // =========================

    glColor3f(0.8, 0.5, 0.2);

    glBegin(GL_QUADS);

    glVertex2f(-0.6, 0.4);
    glVertex2f(0.6, 0.4);
    glVertex2f(0.6, -0.6);
    glVertex2f(-0.6, -0.6);

    glEnd();


    // =========================
    // Roof
    // =========================

    glColor3f(1.0, 0.0, 0.0);

    glBegin(GL_TRIANGLES);

    glVertex2f(-0.7, 0.4);
    glVertex2f(0.7, 0.4);
    glVertex2f(0.0, 0.9);

    glEnd();


    // =========================
    // Door
    // =========================

    glColor3f(0.3, 0.1, 0.0);

    glBegin(GL_QUADS);

    glVertex2f(-0.2, -0.6);
    glVertex2f(0.2, -0.6);
    glVertex2f(0.2, 0.0);
    glVertex2f(-0.2, 0.0);

    glEnd();


    // =========================
    // Window
    // =========================

    glColor3f(0.0, 0.5, 1.0);

    glBegin(GL_QUADS);

    glVertex2f(0.3, 0.2);
    glVertex2f(0.5, 0.2);
    glVertex2f(0.5, 0.0);
    glVertex2f(0.3, 0.0);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("House");

    // Background White
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 3. প্রথমে House Body

House-এর main body একটা Rectangle।

তাই:

```cpp
glBegin(GL_QUADS);
```

ব্যবহার করেছি।

```text
Rectangle
   ↓
GL_QUADS
```

---

# 4. House Body-এর Color

```cpp
glColor3f(0.8, 0.5, 0.2);
```

এখানে:

```text
R = 0.8
G = 0.5
B = 0.2
```

তাই Body একটা brown/orange ধরনের color হবে।

---

# 5. House Body-এর চারটি Vertex

```cpp
glVertex2f(-0.6, 0.4);
glVertex2f(0.6, 0.4);
glVertex2f(0.6, -0.6);
glVertex2f(-0.6, -0.6);
```

এগুলো হলো:

```text
Top Left      = (-0.6, 0.4)

Top Right     = (0.6, 0.4)

Bottom Right  = (0.6, -0.6)

Bottom Left   = (-0.6, -0.6)
```

---

# 6. Coordinate দিয়ে Body বুঝি

```text
        (-0.6,0.4) -------- (0.6,0.4)
             |                   |
             |      BODY         |
             |                   |
        (-0.6,-0.6) ------ (0.6,-0.6)
```

চারটি point:

```text
Top Left
   ↓
Top Right
   ↓
Bottom Right
   ↓
Bottom Left
```

এগুলো connect করলে Rectangle তৈরি হয়।

---


# 7. `glEnd()`

```cpp
glEnd();
```

এর মাধ্যমে Body-এর drawing শেষ।

এখন আমাদের কাছে:

```text
 _________
|         |
|         |
|         |
|_________|
```

আছে।

---

# 8. এবার Roof

House-এর Roof হলো Triangle।

তাই:

```cpp
glBegin(GL_TRIANGLES);
```

ব্যবহার করেছি।

```text
Triangle
   ↓
GL_TRIANGLES
```

---

# 9. Roof-এর Color

```cpp
glColor3f(1.0, 0.0, 0.0);
```

মানে:

```text
R = 1
G = 0
B = 0
```

তাই Roof:

> Red

হবে।

---

# 10. Roof-এর 3 Vertex

```cpp
glVertex2f(-0.7, 0.4);
glVertex2f(0.7, 0.4);
glVertex2f(0.0, 0.9);
```

এগুলো:

```text
Left   = (-0.7, 0.4)

Right  = (0.7, 0.4)

Top    = (0.0, 0.9)
```

---

# 28. Window Move করা

Window-এর:

```cpp
0.3
0.5
```

X coordinate।

এগুলো change করলে Window left/right move করবে।

Y coordinate:

```cpp
0.2
0.0
```

change করলে Window up/down move করবে।

---
# 29. দুইটা Window বানাতে চাইলে

একটা Window-এর code copy করে X coordinate negative করে দিতে পারো।

Existing:

```cpp
glVertex2f(0.3, 0.2);
glVertex2f(0.5, 0.2);
glVertex2f(0.5, 0.0);
glVertex2f(0.3, 0.0);
```

Left Window:

```cpp
glVertex2f(-0.5, 0.2);
glVertex2f(-0.3, 0.2);
glVertex2f(-0.3, 0.0);
glVertex2f(-0.5, 0.0);
```

তাহলে:

```text
       /\
      /  \
     /____\
     | [] [] |
     |       |
     |  __   |
     | |  |  |
     |_|__|__|
```

এরকম হবে।

---

# 30. Door-এর Handle যোগ করা

Door-এর উপর ছোট একটা Point দিতে পারো।

```cpp
glPointSize(8);

glBegin(GL_POINTS);

glColor3f(1,1,0);

glVertex2f(0.12, -0.3);

glEnd();
```

এখানে:

```text
GL_POINTS
   ↓
Door Handle
```

তবে basic exam-এর জন্য এটা optional।

---

# 31. Full House Structure

মনে রাখবে:

```text
             Roof
          GL_TRIANGLES
               ↓
              /\
             /  \
            /____\
               ↓
           House Body
           GL_QUADS
               ↓
         ┌──────────┐
         │  Window  │
         │          │
         │   Door   │
         └──────────┘
```

---

# 32. Exam-এ কীভাবে ভাববে?

Question যদি আসে:

> **Draw a House using OpenGL**

প্রথমে shape ভাগ করবে:

```text
1. Body → Rectangle
2. Roof → Triangle
3. Door → Rectangle
4. Window → Rectangle
```

তারপর primitive:

```text
Rectangle → GL_QUADS
Triangle  → GL_TRIANGLES
```

তারপর coordinate বসাবে।

---


# 33. Viva Questions

### Q1. House কীভাবে তৈরি করা হয়েছে?

**Answer:** Multiple basic shapes combine করে House তৈরি করা হয়েছে।

---

### Q2. House Body-এর জন্য কী ব্যবহার করেছি?

**Answer:** `GL_QUADS`।

---

### Q3. Roof-এর জন্য?

**Answer:** `GL_TRIANGLES`।

---

### Q4. Door-এর জন্য?

**Answer:** `GL_QUADS`।

---

### Q5. Window-এর জন্য?

**Answer:** `GL_QUADS`।

---

### Q6. House-কে Composite Shape বলা হয় কেন?

**Answer:** কারণ একাধিক basic shape একসাথে ব্যবহার করে House তৈরি করা হয়েছে।

---

### Q7. Roof এবং Body কীভাবে connect হয়েছে?

**Answer:** Body-এর top এবং Roof-এর bottom-এর Y coordinate একই রাখা হয়েছে।

```text
Y = 0.4
```

---

### Q8. `glColor3f()` কী করে?

**Answer:** Shape-এর color set করে।

---

### Q9. `glVertex2f()` কী করে?

**Answer:** `(x,y)` coordinate-এ Vertex define করে।

---

### Q10. `GL_QUADS`-এ কয়টি Vertex লাগে?

**Answer:** 4টি Vertex।

---

### Q11. `GL_TRIANGLES`-এ কয়টি Vertex লাগে?

**Answer:** 3টি Vertex।

---


# 34. Common Mistakes

### Mistake 1: Roof-এর bottom আর Body-এর top একই Y না রাখা

Body:

```text
Y = 0.4
```

তাহলে Roof-এর bottom-ও:

```text
Y = 0.4
```

রাখা ভালো।

---

### Mistake 2: Quad-এর Vertex ভুল order

সাধারণভাবে:

```text
Top Left
→ Top Right
→ Bottom Right
→ Bottom Left
```

দিলে সহজে Rectangle তৈরি হয়।

---

### Mistake 3: Door Body-এর বাইরে চলে যাওয়া

Door-এর bottom:

```text
Y = -0.6
```

Body-এর bottom-এর সাথে match করেছে।

---

# 35. Quick Revision

```text
House
 ↓
Composite Shape

Body
 ↓
GL_QUADS

Roof
 ↓
GL_TRIANGLES

Door
 ↓
GL_QUADS

Window
 ↓
GL_QUADS
```

Coordinate rule:

```text
+X → Right
-X → Left

+Y → Up
-Y → Down
```

---

# 36. One-Line Memory Trick

> **House = Rectangle Body + Triangle Roof + Rectangle Door + Rectangle Window।**
