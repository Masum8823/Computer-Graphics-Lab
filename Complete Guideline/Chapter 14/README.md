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
