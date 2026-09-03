# Draw a Star

> OpenGL-এ কয়েকটি Vertex নির্দিষ্টভাবে বসিয়ে এবং `GL_POLYGON` ব্যবহার করে একটি simple 5-point Star আঁকা।

---

# 1. Star কীভাবে আঁকবো?

আমরা একটা 5-point Star বানাতে **10টা Vertex** ব্যবহার করবো।

কেন 10টা?

```text
5টা Outer Point
+
5টা Inner Point
=
10টা Vertex
```

সহজভাবে:

```text
        Outer
          ●
         / \
        /   \
   ●---●     ●---●
    \           /
     ●         ●
      \       /
       ●-----●
```

আসলে আমরা Outer আর Inner point একটার পর একটা দেবো।

---

# 2. Basic Star Code

```cpp
glBegin(GL_POLYGON);

glVertex2f(0.0, 0.8);      // Top Outer
glVertex2f(0.18, 0.25);    // Top Right Inner

glVertex2f(0.76, 0.25);    // Right Outer
glVertex2f(0.29, -0.1);    // Right Inner

glVertex2f(0.47, -0.7);    // Bottom Right Outer
glVertex2f(0.0, -0.3);     // Bottom Inner

glVertex2f(-0.47, -0.7);   // Bottom Left Outer
glVertex2f(-0.29, -0.1);   // Left Inner

glVertex2f(-0.76, 0.25);   // Left Outer
glVertex2f(-0.18, 0.25);   // Top Left Inner

glEnd();
```

এখন একদম সহজ করে বুঝি।

---

# 3. `glBegin(GL_POLYGON)`

```cpp
glBegin(GL_POLYGON);
```

এর মাধ্যমে আমরা বলছি:

> এখন Polygon আঁকা শুরু করবো।

Star-এর জন্য আমরা একাধিক Vertex দেবো।

```text
Multiple Vertex
      ↓
GL_POLYGON
      ↓
Star Shape
```

---

# 4. কেন 10টা Vertex?

একটা 5-point Star-এর:

```text
5টা বাইরের point
```

এবং:

```text
5টা ভিতরের point
```

থাকে।

তাই:

```text
5 + 5 = 10 Vertex
```

---

# 5. Outer Point কী?

Star-এর বাইরের বড় point-গুলোকে বলছি:

```text
Outer Point
```

যেমন:

```cpp
glVertex2f(0.0, 0.8);
```

এটা Star-এর সবচেয়ে উপরের Outer Point।

---

# 6. Inner Point কী?

Star-এর ভিতরের ছোট point-গুলো:

```text
Inner Point
```

যেমন:

```cpp
glVertex2f(0.18, 0.25);
```

এটা Top-এর Outer Point-এর পরের Inner Point।

---

# 7. Vertex Order খুব Important

Star আঁকার সময় আমরা এই pattern follow করছি:

```text
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
...
```

অর্থাৎ:

```text
O → I → O → I → O → I → O → I → O → I
```

এখানে:

```text
O = Outer Point
I = Inner Point
```

এটাই Star-এর সবচেয়ে important concept।

---


# 8. প্রথম Vertex

```cpp
glVertex2f(0.0, 0.8);
```

এটা:

```text
X = 0.0
Y = 0.8
```

তাই point-টা:

```text
Center-এর উপরে
```

থাকবে।

এটাই Star-এর **Top Outer Point**।

---

# 9. দ্বিতীয় Vertex

```cpp
glVertex2f(0.18, 0.25);
```

এটা:

```text
X = 0.18
Y = 0.25
```

এটা Top-এর একটু নিচে এবং ডানদিকে।

এটা:

> **Top Right Inner Point**

---

# 10. তৃতীয় Vertex

```cpp
glVertex2f(0.76, 0.25);
```

এটা Star-এর ডানদিকে থাকা Outer Point।

```text
X = 0.76
Y = 0.25
```

তাই:

> **Right Outer Point**

---

# 11. চতুর্থ Vertex

```cpp
glVertex2f(0.29, -0.1);
```

এটা Right Outer Point-এর পরে ভিতরের দিকে আসে।

তাই:

> **Right Inner Point**

---

# 12. পঞ্চম Vertex

```cpp
glVertex2f(0.47, -0.7);
```

এটা:

> **Bottom Right Outer Point**

---

# 13. ষষ্ঠ Vertex

```cpp
glVertex2f(0.0, -0.3);
```

এটা Star-এর নিচের মাঝামাঝি Inner Point।

তাই:

> **Bottom Inner Point**

---

# 14. সপ্তম Vertex

```cpp
glVertex2f(-0.47, -0.7);
```

এটা:

> **Bottom Left Outer Point**

কারণ X negative হওয়ায় এটা বামদিকে।

---

# 15. অষ্টম Vertex

```cpp
glVertex2f(-0.29, -0.1);
```

এটা:

> **Left Inner Point**

---


# 16. নবম Vertex

```cpp
glVertex2f(-0.76, 0.25);
```

এটা:

> **Left Outer Point**

---

# 17. দশম Vertex

```cpp
glVertex2f(-0.18, 0.25);
```

এটা:

> **Top Left Inner Point**

এরপর:

```cpp
glEnd();
```

দিয়ে drawing শেষ।

---

# 18. Coordinate বুঝে Star আঁকা

আমাদের points:

```text
             (0,0.8)
                ●
               / \
              /   \
   (-0.18,0.25)  (0.18,0.25)
        ●            ●
       /              \
      ●                ●
(-0.76,0.25)      (0.76,0.25)
       \              /
        ●            ●
 (-0.29,-0.1)   (0.29,-0.1)
          \      /
           ●    ●
      (-0.47,-0.7) (0.47,-0.7)
```

এটা concept বোঝানোর জন্য।

---

# 19. Star-এর Vertex Order

আমাদের order:

```text
1 → Top Outer

2 → Top Right Inner

3 → Right Outer

4 → Right Inner

5 → Bottom Right Outer

6 → Bottom Inner

7 → Bottom Left Outer

8 → Left Inner

9 → Left Outer

10 → Top Left Inner
```

অর্থাৎ:

```text
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
 ↓
Outer
 ↓
Inner
```

---


# 20. Star-এর Size কীভাবে Change করবো?

যেমন:

```cpp
glVertex2f(0.0, 0.8);
```

এখানে `0.8` হলো Top Point-এর distance।

এটা যদি:

```cpp
glVertex2f(0.0, 0.5);
```

করো, Star ছোট হবে।

আর:

```cpp
glVertex2f(0.0, 0.9);
```

করলে বড় হবে।

তবে শুধু একটা coordinate change করলে shape একটু distorted হতে পারে।

তাই পুরো Star বড়/ছোট করতে সব coordinate proportionally change করা ভালো।

---



# 21. Star-এর Position Change

ধরো Star-কে ডানদিকে নিতে চাই।

তাহলে সব X coordinate-এর সাথে একটি value যোগ করতে পারো।

Concept:

```text
x = x + centerX
y = y + centerY
```

তবে beginner lab-এর জন্য manually coordinate change করলেই যথেষ্ট।

---

# 22. Star-এর Color

Star-এর আগে:

```cpp
glColor3f(1.0, 0.0, 0.0);
```

দিলে Star Red হবে।

```cpp
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POLYGON);

glVertex2f(0.0, 0.8);
glVertex2f(0.18, 0.25);
glVertex2f(0.76, 0.25);
glVertex2f(0.29, -0.1);
glVertex2f(0.47, -0.7);
glVertex2f(0.0, -0.3);
glVertex2f(-0.47, -0.7);
glVertex2f(-0.29, -0.1);
glVertex2f(-0.76, 0.25);
glVertex2f(-0.18, 0.25);

glEnd();
```

---

# 23. Star-এর Different Color

Triangle-এর মতো প্রতিটি Vertex-এর আগে আলাদা Color দিলে color change হতে পারে।

```cpp
glBegin(GL_POLYGON);

glColor3f(1,0,0);
glVertex2f(0.0,0.8);

glColor3f(0,1,0);
glVertex2f(0.18,0.25);

glColor3f(0,0,1);
glVertex2f(0.76,0.25);

glColor3f(1,1,0);
glVertex2f(0.29,-0.1);

glColor3f(1,0,1);
glVertex2f(0.47,-0.7);

glColor3f(0,1,1);
glVertex2f(0.0,-0.3);

glColor3f(1,0,0);
glVertex2f(-0.47,-0.7);

glColor3f(0,1,0);
glVertex2f(-0.29,-0.1);

glColor3f(0,0,1);
glVertex2f(-0.76,0.25);

glColor3f(1,1,0);
glVertex2f(-0.18,0.25);

glEnd();
```

তবে lab exam-এর basic Star-এর জন্য **একটা color রাখাই সহজ**।

---

# 24. Full Simple Program

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Star-এর Color
    glColor3f(1.0, 1.0, 0.0);

    // Polygon শুরু
    glBegin(GL_POLYGON);

    // Top Outer
    glVertex2f(0.0, 0.8);

    // Top Right Inner
    glVertex2f(0.18, 0.25);

    // Right Outer
    glVertex2f(0.76, 0.25);

    // Right Inner
    glVertex2f(0.29, -0.1);

    // Bottom Right Outer
    glVertex2f(0.47, -0.7);

    // Bottom Inner
    glVertex2f(0.0, -0.3);

    // Bottom Left Outer
    glVertex2f(-0.47, -0.7);

    // Left Inner
    glVertex2f(-0.29, -0.1);

    // Left Outer
    glVertex2f(-0.76, 0.25);

    // Top Left Inner
    glVertex2f(-0.18, 0.25);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Star");

    // Background Black
    glClearColor(0.0, 0.0, 0.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 25. Code Flow

```text
glClear()
   ↓
Screen Clear

glColor3f()
   ↓
Color Set

glBegin(GL_POLYGON)
   ↓
Drawing Start

Outer Point
   ↓
Inner Point
   ↓
Outer Point
   ↓
Inner Point
   ↓
...
   ↓
10 Vertex

glEnd()
   ↓
Drawing Finish

glFlush()
   ↓
Output
```

---
