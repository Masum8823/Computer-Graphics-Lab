# Translation

> Translation হলো কোনো object/shape-কে **এক জায়গা থেকে অন্য জায়গায় move করা**, কিন্তু shape-এর size বা angle পরিবর্তন হয় না।

---

# 1. Translation কী?

সহজ ভাষায়:

```text
Object
  ↓
Move
  ↓
New Position
```

যেমন:

```text
আগে                 পরে

  ■                    ■
                     →
```

Square-এর shape একই থাকবে, শুধু position change হবে।

---

# 2. Translation-এর Basic Formula

একটি point যদি হয়:

```text
(x, y)
```

Translation-এর পরে:

```text
x' = x + Tx
y' = y + Ty
```

এখানে:

```text
Tx = X direction-এ কতটুকু move করবে
Ty = Y direction-এ কতটুকু move করবে
```

---

# 3. সহজ Example

ধরি একটি point:

```text
(0.2, 0.3)
```

এখন:

```text
Tx = 0.4
Ty = 0.2
```

দিলে:

```text
x' = 0.2 + 0.4
   = 0.6

y' = 0.3 + 0.2
   = 0.5
```

নতুন point:

```text
(0.6, 0.5)
```

অর্থাৎ Point-টা Right এবং Up দিকে গেছে।

---

# 4. OpenGL-এ Translation

OpenGL-এ Translation করার জন্য:

```cpp
glTranslatef(Tx, Ty, 0);
```

ব্যবহার করা যায়।

এখানে:

```text
Tx → X direction
Ty → Y direction
0  → Z direction
```

আমরা 2D graphics করছি, তাই Z = `0` রাখবো।

---

# 5. Simple Translation Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Translation শুরু
    // Object-কে X দিকে 0.4
    // এবং Y দিকে 0.2 move করবে
    glTranslatef(0.4, 0.2, 0.0);

    // Object-এর Color
    glColor3f(1.0, 0.0, 0.0);

    // একটি Rectangle draw করছি
    glBegin(GL_QUADS);

    glVertex2f(-0.2, 0.2);
    glVertex2f(0.2, 0.2);
    glVertex2f(0.2, -0.2);
    glVertex2f(-0.2, -0.2);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Translation");

    // Background Color
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---


# 6. `glTranslatef()` বুঝি

সবচেয়ে important line:

```cpp
glTranslatef(0.4, 0.2, 0.0);
```

এখানে:

```text
0.4 → X direction-এ move

0.2 → Y direction-এ move

0.0 → Z direction-এ move
```

তাই:

```text
X positive → Right
Y positive → Up
```

Object:

```text
Right + Up
```

দিকে যাবে।

---

# 7. Translation-এর আগে Rectangle

আমাদের Rectangle:

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.2, 0.2);
glVertex2f(0.2, 0.2);
glVertex2f(0.2, -0.2);
glVertex2f(-0.2, -0.2);

glEnd();
```

এর Center:

```text
(0,0)
```

এরকম:

```text
       Y
       ↑
       |
    ┌─────┐
    │     │
    │  ■  │
    │     │
    └─────┘
       |
-------+------------→ X
```

---


# 8. Translation-এর পরে

আমরা লিখেছি:

```cpp
glTranslatef(0.4, 0.2, 0.0);
```

তাই Rectangle:

```text
X → +0.4
Y → +0.2
```

move করবে।

```text
আগে                 পরে

  ■                    ■
                       ↗
```

অর্থাৎ Right এবং Up দিকে গেছে।

---


# 9. খুব Important Concept

Translation shape-এর coordinate **change করে না**, বরং object-এর পুরো coordinate system-কে shift করে।

Exam-এর জন্য সহজভাবে মনে রাখো:

> `glTranslatef()` object-কে এক position থেকে অন্য position-এ move করে।

---

# 10. শুধু Right দিকে নিতে চাইলে

```cpp
glTranslatef(0.5, 0.0, 0.0);
```

এখানে:

```text
Tx = 0.5
Ty = 0
```

তাই:

```text
→ Right
```

দিকে যাবে।

---

# 11. শুধু Left দিকে নিতে চাইলে

```cpp
glTranslatef(-0.5, 0.0, 0.0);
```

কারণ:

```text
-X → Left
```

তাই object Left দিকে যাবে।

---

# 12. শুধু Up দিকে নিতে চাইলে

```cpp
glTranslatef(0.0, 0.5, 0.0);
```

কারণ:

```text
+Y → Up
```

---

# 13. শুধু Down দিকে নিতে চাইলে

```cpp
glTranslatef(0.0, -0.5, 0.0);
```

কারণ:

```text
-Y → Down
```

---

# 14. চার Direction মনে রাখো

```text
             +Y
              ↑
              |
       -X ←---+---→ +X
              |
              ↓
             -Y
```

তাই:

```text
+X → Right
-X → Left
+Y → Up
-Y → Down
```

---

# 15. Translation-এর Formula

যদি:

```text
Original Point = (x,y)
```

এবং:

```text
Tx = 0.3
Ty = 0.2
```

তাহলে:

```text
x' = x + 0.3
y' = y + 0.2
```

---

# 16. Example

ধরি:

```text
Point = (-0.2, 0.1)
```

Translation:

```text
Tx = 0.4
Ty = 0.3
```

তাহলে:

```text
x' = -0.2 + 0.4
   = 0.2

y' = 0.1 + 0.3
   = 0.4
```

New Point:

```text
(0.2, 0.4)
```

---

# 17. Rectangle-এর ক্ষেত্রে কী হবে?

ধরি Rectangle-এর points:

```text
(-0.2, 0.2)
(0.2, 0.2)
(0.2,-0.2)
(-0.2,-0.2)
```

Translation:

```text
Tx = 0.4
Ty = 0.2
```

তাহলে প্রতিটি point-এর সাথে `0.4` এবং `0.2` যোগ হবে।

### Point 1:

```text
(-0.2, 0.2)

x' = -0.2 + 0.4 = 0.2
y' =  0.2 + 0.2 = 0.4

New = (0.2, 0.4)
```

### Point 2:

```text
(0.2, 0.2)

New = (0.6, 0.4)
```

### Point 3:

```text
(0.2,-0.2)

New = (0.6, 0.0)
```

### Point 4:

```text
(-0.2,-0.2)

New = (0.2, 0.0)
```

তাই পুরো Rectangle একই shape রেখে move করবে।

---

# 18. Translation-এ Shape-এর কী Change হয়?

Translation করলে:

```text
Shape Size     → Same
Shape Angle    → Same
Shape Shape    → Same
Position       → Change
```

অর্থাৎ:

```text
Translation = Position Change
```

---

# 19. Translation-এ Size Change হয় না

ধরি একটা Rectangle:

```text
Width  = 0.4
Height = 0.4
```

Translation করার পরেও:

```text
Width  = 0.4
Height = 0.4
```

থাকবে।

শুধু জায়গা পরিবর্তন করবে।

---

# 20. `glTranslatef()`-এর 3টি Parameter

```cpp
glTranslatef(Tx, Ty, Tz);
```

মানে:

```text
1st → X movement
2nd → Y movement
3rd → Z movement
```

2D graphics-এর ক্ষেত্রে:

```cpp
glTranslatef(Tx, Ty, 0.0);
```

---

# 21. `glPushMatrix()` এবং `glPopMatrix()`

Translation-এর সময় একটা important ব্যাপার আছে।

ধরি:

```cpp
glTranslatef(0.5, 0.0, 0.0);
```

তারপর আরও একটা object draw করলে সেই object-ও translated position পেতে পারে।

এটা prevent করতে:

```cpp
glPushMatrix();

glTranslatef(0.5, 0.0, 0.0);

// Object

glPopMatrix();
```

ব্যবহার করা যায়।

---

# 22. `glPushMatrix()` কী করে?

```cpp
glPushMatrix();
```

বর্তমান transformation state save করে রাখে।

সহজ ভাষায়:

> বর্তমান অবস্থাটা মনে রাখে।

---

# 23. `glPopMatrix()` কী করে?

```cpp
glPopMatrix();
```

আগে save করা অবস্থায় ফিরে যায়।

সহজ ভাষায়:

> আগের অবস্থায় ফিরে যায়।

---

# 24. Safe Translation Structure

Exam-এর জন্য এই structure মনে রাখতে পারো:

```cpp
glPushMatrix();

glTranslatef(0.4, 0.2, 0.0);

// Draw Object

glPopMatrix();
```

Flow:

```text
Save
 ↓
Translate
 ↓
Draw
 ↓
Restore
```

---

# 25. Example with Push/Pop

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Current transformation save
    glPushMatrix();

    // Object-কে Right এবং Up দিকে move
    glTranslatef(0.4, 0.2, 0.0);

    // Red Color
    glColor3f(1.0, 0.0, 0.0);

    // Rectangle
    glBegin(GL_QUADS);

    glVertex2f(-0.2, 0.2);
    glVertex2f(0.2, 0.2);
    glVertex2f(0.2, -0.2);
    glVertex2f(-0.2, -0.2);

    glEnd();

    // আগের transformation-এ ফিরে যাওয়া
    glPopMatrix();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Translation");

    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 26. দুইটা Object থাকলে

ধরি:

```text
Object 1 → Right
Object 2 → Left
```

তাহলে:

```cpp
// Object 1
glPushMatrix();

glTranslatef(0.5, 0.0, 0.0);

// Draw Object 1

glPopMatrix();


// Object 2
glPushMatrix();

glTranslatef(-0.5, 0.0, 0.0);

// Draw Object 2

glPopMatrix();
```

এখানে দুই Object আলাদাভাবে move করবে।

---

# 27. কেন `Push/Pop` ব্যবহার করি?

ধরি:

```cpp
glTranslatef(0.5, 0.0, 0.0);
```

করার পর Object 1 draw করলাম।

তারপর Object 2 draw করলাম।

তাহলে Object 2-ও সেই transformation পেয়ে যেতে পারে।

তাই:

```text
glPushMatrix()
       ↓
Translation
       ↓
Object Draw
       ↓
glPopMatrix()
```

করলে transformation আলাদা রাখা যায়।

---
