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
