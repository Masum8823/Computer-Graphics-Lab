# Draw a Polygon

> OpenGL-এ একাধিক Vertex ব্যবহার করে একটি closed shape তৈরি করার basic method।

---

# 1. Polygon কী?

Polygon মানে হলো **একাধিক straight line দিয়ে তৈরি একটি closed shape**।

যেমন:

```text
Triangle    → 3 sides
Rectangle   → 4 sides
Pentagon    → 5 sides
Hexagon     → 6 sides
```

সহজভাবে:

```text
3 Vertex → Triangle
4 Vertex → Quadrilateral
5 Vertex → Pentagon
6 Vertex → Hexagon
```

---

# 2. Polygon আঁকার জন্য কী ব্যবহার করবো?

OpenGL-এ:

```cpp
glBegin(GL_POLYGON);
```

ব্যবহার করা হয়।

```text
GL_POLYGON
     ↓
Polygon Drawing Mode
```

---

# 3. Basic Polygon Code

একটা simple Pentagon আঁকি:

```cpp
glBegin(GL_POLYGON);

glVertex2f(0.0, 0.7);
glVertex2f(0.6, 0.3);
glVertex2f(0.4, -0.5);
glVertex2f(-0.4, -0.5);
glVertex2f(-0.6, 0.3);

glEnd();
```

এখানে:

```text
5 Vertex
   ↓
5-sided Polygon
   ↓
Pentagon
```

---

# 4. `glBegin(GL_POLYGON)`

```cpp
glBegin(GL_POLYGON);
```

এখানে OpenGL-কে বলা হচ্ছে:

> এখন আমরা Polygon আঁকবো।

এরপর যতগুলো:

```cpp
glVertex2f()
```

দেবো, সেগুলো Polygon-এর corner/vertex হিসেবে কাজ করবে।

---


# 5. Polygon-এর Vertex কীভাবে কাজ করে?

ধরো:

```cpp
glVertex2f(0.0, 0.7);
glVertex2f(0.6, 0.3);
glVertex2f(0.4, -0.5);
glVertex2f(-0.4, -0.5);
glVertex2f(-0.6, 0.3);
```

এগুলোকে:

```text
Vertex 1
   ↓
Vertex 2
   ↓
Vertex 3
   ↓
Vertex 4
   ↓
Vertex 5
   ↓
আবার Vertex 1
```

connect করা হয়।

তাই closed shape তৈরি হয়।

---

# 6. Diagram

আমাদের Pentagon:

```text
                 ●
              (0,0.7)
               /   \
              /     \
             /       \
            ●         ●
      (-0.6,0.3)   (0.6,0.3)
            |         |
            |         |
            ●─────────●
       (-0.4,-0.5) (0.4,-0.5)
```

এখানে ৫টি Vertex আছে।

তাই এটি:

> **Pentagon**

---

# 7. Vertex Count অনুযায়ী Polygon

এটা খুব সহজে মনে রাখবে:

```text
3 Vertex → Triangle

4 Vertex → Quadrilateral

5 Vertex → Pentagon

6 Vertex → Hexagon

7 Vertex → Heptagon

8 Vertex → Octagon
```

অর্থাৎ:

> Vertex যতগুলো, Polygon-এর side-ও সাধারণত ততগুলো।

---


# 8. `GL_POLYGON` + Color

Polygon-এর color দিতে:

```cpp
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POLYGON);

glVertex2f(0.0, 0.7);
glVertex2f(0.6, 0.3);
glVertex2f(0.4, -0.5);
glVertex2f(-0.4, -0.5);
glVertex2f(-0.6, 0.3);

glEnd();
```

এখানে পুরো Polygon হবে:

> **Red**

---

# 9. Polygon-এর Vertex-এর আলাদা Color

আগের Triangle-এর মতো Polygon-এর প্রতিটি Vertex-এ আলাদা color-ও দেওয়া যায়।

```cpp
glBegin(GL_POLYGON);

glColor3f(1,0,0);
glVertex2f(0.0,0.7);

glColor3f(0,1,0);
glVertex2f(0.6,0.3);

glColor3f(0,0,1);
glVertex2f(0.4,-0.5);

glColor3f(1,1,0);
glVertex2f(-0.4,-0.5);

glColor3f(1,0,1);
glVertex2f(-0.6,0.3);

glEnd();
```

তাহলে বিভিন্ন Vertex-এর color আলাদা হবে এবং ভিতরের অংশে color blend হতে পারে।

---

# 10. Polygon-এর Coordinate কীভাবে ঠিক করবো?

Polygon-এর প্রতিটি Vertex-এর coordinate manually দিতে পারি।

যেমন Pentagon-এর জন্য:

```text
Top
 ↓
(0, 0.7)

Top Right
 ↓
(0.6, 0.3)

Bottom Right
 ↓
(0.4, -0.5)

Bottom Left
 ↓
(-0.4, -0.5)

Top Left
 ↓
(-0.6, 0.3)
```

তারপর:

```text
Top
 ↓
Top Right
 ↓
Bottom Right
 ↓
Bottom Left
 ↓
Top Left
 ↓
Top
```

এভাবে closed shape হবে।

---

# 11. সবচেয়ে Important Rule: Vertex Order

Polygon-এর ক্ষেত্রে **Vertex order খুব important**।

ধরো আমরা এইভাবে দিচ্ছি:

```text
1 → 2 → 3 → 4 → 5
```

তাহলে OpenGL সেই order follow করবে।

ভালো practice:

> **একদিক থেকে শুরু করে চারপাশ ঘুরে Vertex দাও।**

যেমন:

```text
Top
 ↓
Top Right
 ↓
Bottom Right
 ↓
Bottom Left
 ↓
Top Left
```

এতে shape সুন্দরভাবে তৈরি হবে।

---

# 12. তোমার Circle Code-এর সাথে Connection

তুমি আগে যে Circle code করেছিলে:

```cpp
glBegin(GL_POLYGON);

for(int i = 0; i < 360; i++)
{
    float angle = i * 3.1416 / 180.0;

    float x = -0.1 + 0.25 * cos(angle);
    float y =  0.0 + 0.25 * sin(angle);

    glVertex2f(x, y);
}

glEnd();
```

এটাও আসলে:

```text
GL_POLYGON
```

ব্যবহার করছে।

তাই এটা **Polygon দিয়েই circle-এর মতো shape বানাচ্ছে।**

---

# 13. Circle Code-এ এতগুলো Vertex কেন?

আমরা করেছিলাম:

```cpp
for(int i = 0; i < 360; i++)
```

অর্থাৎ:

```text
i = 0
1
2
3
...
359
```

মোট:

```text
360 Vertex
```

তাই OpenGL অনেকগুলো ছোট straight line connect করে একটি **circle-এর মতো smooth shape** তৈরি করে।

Concept:

```text
কম Vertex
    ↓
কম smooth

বেশি Vertex
    ↓
বেশি smooth
```

---

# 14. Circle আসলে Polygon-এর মতো কেন?

খুব সহজভাবে:

```text
5 Vertex
 ↓
Pentagon

10 Vertex
 ↓
More rounded shape

100 Vertex
 ↓
অনেক বেশি rounded

360 Vertex
 ↓
Circle-এর মতো smooth
```

অর্থাৎ:

> **অনেকগুলো ছোট straight line-এর combination আমাদের চোখে প্রায় circle-এর মতো দেখায়।**

---

# 15. Circle Code-এর `cos()` ও `sin()` কেন?

Circle-এর point বের করার জন্য:

```cpp
float x = centerX + radius * cos(angle);
float y = centerY + radius * sin(angle);
```

এখানে:

```text
centerX
   ↓
Circle কোথায় থাকবে

centerY
   ↓
Circle কোথায় থাকবে

radius
   ↓
Circle কত বড়

angle
   ↓
কোন position-এর point বের করছি
```

তাই circle-এর চারপাশে point generate করা যায়।

---

# 16. Circle-এর Radius-এর সাথে Polygon-এর Relation

ধরো:

```cpp
radius = 0.25;
```

এখানে `0.25` হলো center থেকে edge পর্যন্ত distance।

```text
Center ●────────● Edge
       ← 0.25 →
```

আর:

```cpp
i < 360
```

দিয়ে আমরা 360 degree ঘুরছি।

```text
0° → 360°
```

এভাবে circle-এর চারপাশের অনেকগুলো point পাই।

---

# 17. Polygon vs Circle

| Polygon                     | Circle-like Shape                             |
| --------------------------- | --------------------------------------------- |
| কম Vertex হতে পারে          | অনেক Vertex                                   |
| Straight sides দেখা যায়     | অনেক smooth                                   |
| `GL_POLYGON`                | `GL_POLYGON`                                  |
| Manual coordinate দেওয়া যায় | `sin()` + `cos()` দিয়ে point generate করা যায় |

Example:

```text
5 Vertex
   ↓
Pentagon

20 Vertex
   ↓
অনেকটা rounded

360 Vertex
   ↓
Circle-এর মতো
```

---

# 18. Polygon-এর Size Change

Pentagon:

```cpp
glVertex2f(0.0, 0.7);
glVertex2f(0.6, 0.3);
glVertex2f(0.4, -0.5);
glVertex2f(-0.4, -0.5);
glVertex2f(-0.6, 0.3);
```

এগুলোকে বড় করলে:

```cpp
glVertex2f(0.0, 0.9);
glVertex2f(0.8, 0.4);
glVertex2f(0.6, -0.7);
glVertex2f(-0.6, -0.7);
glVertex2f(-0.8, 0.4);
```

Polygon বড় হবে।

কারণ Vertexগুলো center থেকে দূরে গেছে।

---

# 19. Polygon-এর Position Change

সব coordinate-এর X value positive করলে shape ডানদিকে যাবে।

Example:

```cpp
glVertex2f(0.4, 0.7);
glVertex2f(1.0, 0.3);
glVertex2f(0.8, -0.5);
glVertex2f(0.0, -0.5);
glVertex2f(-0.2, 0.3);
```

তবে coordinate যেন window-এর visible range-এর বাইরে বেশি চলে না যায়।

---

# 20. Complete Pentagon Program

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    glColor3f(1.0, 0.0, 0.0);

    glBegin(GL_POLYGON);

    glVertex2f(0.0, 0.7);
    glVertex2f(0.6, 0.3);
    glVertex2f(0.4, -0.5);
    glVertex2f(-0.4, -0.5);
    glVertex2f(-0.6, 0.3);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Polygon");

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
Screen Clear

glColor3f()
   ↓
Polygon Color

glBegin(GL_POLYGON)
   ↓
Polygon Mode

glVertex2f()
   ↓
Vertex 1

glVertex2f()
   ↓
Vertex 2

glVertex2f()
   ↓
Vertex 3

glVertex2f()
   ↓
Vertex 4

glVertex2f()
   ↓
Vertex 5

glEnd()
   ↓
Drawing শেষ

glFlush()
   ↓
Output
```

---
