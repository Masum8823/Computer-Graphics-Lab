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