# Draw a Stickman

> Stickman হলো কয়েকটি basic shape/line একসাথে ব্যবহার করে বানানো একটি simple human figure।

---

# 1. Stickman কীভাবে বানাবো?

একটা Stickman বানাতে মূলত:

```text
Circle → Head

Line → Body

Line → দুই হাত

Line → দুই পা
```

অর্থাৎ:

```text id="t7s4xk"
       Circle
         ↓
        Head

         |
         |
         |
        Body

      /     \
     /       \
   Arms

     /   \
    /     \
  Legs
```

এখানে আমরা **Circle + Lines** ব্যবহার করবো।

---


# 2. আমাদের Stickman

আমাদের Stickman-এর structure:

```text id="n7h1pz"
       O
       |
    ---|---
       |
      / \
     /   \
```

এখানে:

```text id="v2j5kk"
 O      → Head
 |      → Body
---     → Arms
/ \     → Legs
```

---

# 3. Simple Stickman Code

```cpp id="1cnm1m"
#include <GL/glut.h>
#include <math.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Black color
    glColor3f(0.0, 0.0, 0.0);

    // =====================
    // Head
    // =====================

    glBegin(GL_POLYGON);

    for(int i = 0; i < 360; i++)
    {
        float angle = i * 3.1416 / 180.0;

        float x = 0.0 + 0.2 * cos(angle);
        float y = 0.5 + 0.2 * sin(angle);

        glVertex2f(x, y);
    }

    glEnd();


    // =====================
    // Body + Arms + Legs
    // =====================

    glBegin(GL_LINES);

    // Body
    glVertex2f(0.0, 0.3);
    glVertex2f(0.0, -0.3);

    // Left Arm
    glVertex2f(0.0, 0.15);
    glVertex2f(-0.4, -0.05);

    // Right Arm
    glVertex2f(0.0, 0.15);
    glVertex2f(0.4, -0.05);

    // Left Leg
    glVertex2f(0.0, -0.3);
    glVertex2f(-0.3, -0.7);

    // Right Leg
    glVertex2f(0.0, -0.3);
    glVertex2f(0.3, -0.7);

    glEnd();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Stickman");

    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---


# 4. প্রথমে Head বুঝি

Head-এর জন্য আমরা Circle-এর আগের code ব্যবহার করছি।

```cpp id="b1e2j3"
glBegin(GL_POLYGON);
```

এখানে:

> Polygon drawing শুরু।

তারপর:

```cpp id="6o7q5v"
for(int i = 0; i < 360; i++)
```

মানে:

> 0 থেকে 359 degree পর্যন্ত ঘুরবো।

---

# 5. Angle

```cpp id="6x8y5e"
float angle = i * 3.1416 / 180.0;
```

এটা:

```text id="8m5g4r"
Degree → Radian
```

convert করছে।

কারণ:

```cpp id="px2p6g"
sin()
cos()
```

এর জন্য Radian দরকার।

---

# 6. Head-এর X Coordinate

```cpp id="5o2m6z"
float x = 0.0 + 0.2 * cos(angle);
```

এখানে:

```text id="0w8l8d"
0.0 → Center X
0.2 → Radius
```

তাই Head-এর center:

```text id="l5d1oq"
X = 0.0
```

এবং Head-এর radius:

```text id="2vpgv8"
0.2
```

---

# 7. Head-এর Y Coordinate

```cpp id="m2j9pu"
float y = 0.5 + 0.2 * sin(angle);
```

এখানে:

```text id="b2c4a7"
0.5 → Center Y
0.2 → Radius
```

অর্থাৎ Head-এর center:

```text id="p9j3in"
(0.0, 0.5)
```

---


# 8. Head-এর Position

আমাদের:

```cpp id="j48d71"
float x = 0.0 + 0.2 * cos(angle);
float y = 0.5 + 0.2 * sin(angle);
```

তাই:

```text id="9o7r9f"
Center = (0.0, 0.5)
Radius = 0.2
```

অর্থাৎ Head window-এর মাঝামাঝি উপরের দিকে থাকবে।

---

# 9. `glVertex2f(x,y)`

```cpp id="k8f8g1"
glVertex2f(x, y);
```

এখানে Circle-এর প্রতিটি point তৈরি হচ্ছে।

```text id="q4h4df"
angle
  ↓
x calculate
  ↓
y calculate
  ↓
glVertex2f(x,y)
  ↓
Point
```

অনেক point:

```text id="z0m8vy"
360 Point
   ↓
GL_POLYGON
   ↓
Head/Circle
```

---

# 10. Head শেষ

```cpp id="m9t1qx"
glEnd();
```

এখানে Head-এর Polygon drawing শেষ।

তখন আমাদের কাছে:

```text id="v4n0ae"
       O
```

আছে।

---

# 11. এবার Body

Body-এর জন্য:

```cpp id="d9x2p4"
glBegin(GL_LINES);
```

ব্যবহার করবো।

কারণ Body একটা straight line।

```text id="1s4t2b"
GL_LINES
   ↓
2 Vertex
   ↓
1 Line
```

---

# 12. Body Line

```cpp id="r6m1os"
glVertex2f(0.0, 0.3);
glVertex2f(0.0, -0.3);
```

এখানে:

```text id="i4qj8g"
Start = (0.0, 0.3)

End = (0.0, -0.3)
```

দুই point connect হবে।

তাই:

```text id="0byxpv"
       O
       |
       |
       |
```

এটাই Body।

---

# 13. Body কেন `x = 0.0`?

Body:

```cpp id="0d2u5g"
(0.0, 0.3)
(0.0, -0.3)
```

দুটোর X একই:

```text id="p9g2dg"
X = 0.0
```

তাই line vertical হবে।

```text id="c5ap7j"
X same
 ↓
Vertical Line
```

---

# 14. Left Arm

```cpp id="z2p4m9"
glVertex2f(0.0, 0.15);
glVertex2f(-0.4, -0.05);
```

Start:

```text id="4w5k3q"
(0.0, 0.15)
```

End:

```text id="3x1p7s"
(-0.4, -0.05)
```

X negative হওয়ায় line:

```text id="t9m3q7"
Left side
```

যাবে।

তাই:

```text id="gj4w42"
       |
      /
     /
```

---
