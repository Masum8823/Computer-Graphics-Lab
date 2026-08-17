# Draw a Triangle

> OpenGL-এ ৩টি Vertex ব্যবহার করে একটি Triangle আঁকার basic method।

---

# 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* `GL_TRIANGLES` কী
* Triangle-এর জন্য কয়টি Vertex লাগে
* ৩টি coordinate কীভাবে Triangle তৈরি করে
* `glColor3f()` দিয়ে প্রতিটি Vertex-এর আলাদা Color দেওয়া
* Triangle-এর position পরিবর্তন করা

---

# 2. Basic Triangle Code

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এখানে মোট **৩টি Vertex** আছে।

```text
3 Vertex → 1 Triangle
```

---

# 3. `glBegin(GL_TRIANGLES)`

```cpp
glBegin(GL_TRIANGLES);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Triangle আঁকবো**।

এখানে:

```text
GL_TRIANGLES
      ↓
Triangle Drawing Mode
```

---

# 4. প্রথম Vertex

```cpp
glVertex2f(0.0, 0.5);
```

Coordinate:

```text
x = 0.0
y = 0.5
```

তাই Point হবে:

> **উপরে / Top**

```text
              ● (0,0.5)
```

---

# 5. দ্বিতীয় Vertex

```cpp
glVertex2f(-0.5, -0.5);
```

এখানে:

```text
x = -0.5 → Left
y = -0.5 → Down
```

তাই Point হবে:

> **Bottom Left**

```text
(-0.5,-0.5) ●
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

তাই Point হবে:

> **Bottom Right**

```text
(0.5,-0.5) ●
```

---

# 7. তিনটি Point কীভাবে Triangle হলো?

আমাদের তিনটি Point:

```text
             (0,0.5)
                ●
               / \
              /   \
             /     \
            /       \
           ●---------●
      (-0.5,-0.5)  (0.5,-0.5)
```

OpenGL তিনটি Vertex-কে **connect** করে।

তাই:

```text
Vertex 1 → Vertex 2
Vertex 2 → Vertex 3
Vertex 3 → Vertex 1
```

এবং একটি closed Triangle তৈরি হয়।

---

# 8. Triangle-এর সবচেয়ে Important Rule

```text
3 Vertex → 1 Triangle
```

অর্থাৎ:

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(x1, y1);
glVertex2f(x2, y2);
glVertex2f(x3, y3);

glEnd();
```

এই তিনটি coordinate মিলে একটি Triangle তৈরি করবে।

---

# 9. Triangle-এর Color

এখন আমাদের আগের code:

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এর সাথে Color যোগ করি।

```cpp
glBegin(GL_TRIANGLES);

glColor3f(1,0,0);
glVertex2f(0.0,0.5);

glColor3f(0,1,0);
glVertex2f(-0.5,-0.5);

glColor3f(0,0,1);
glVertex2f(0.5,-0.5);

glEnd();
```

---

# 10. প্রথম Vertex-এর Color

```cpp
glColor3f(1,0,0);
glVertex2f(0.0,0.5);
```

এখানে:

```text
glColor3f(1,0,0)
        ↓
Red
```

তাই Top Vertex-এর Color **Red**।

---

# 11. দ্বিতীয় Vertex-এর Color

```cpp
glColor3f(0,1,0);
glVertex2f(-0.5,-0.5);
```

এখানে:

```text
glColor3f(0,1,0)
        ↓
Green
```

তাই Bottom Left Vertex-এর Color **Green**।

---

# 12. তৃতীয় Vertex-এর Color

```cpp
glColor3f(0,0,1);
glVertex2f(0.5,-0.5);
```

এখানে:

```text
glColor3f(0,0,1)
        ↓
Blue
```

তাই Bottom Right Vertex-এর Color **Blue**।

---


# 13. Full Colored Triangle

```cpp
glBegin(GL_TRIANGLES);

glColor3f(1,0,0);
glVertex2f(0.0,0.5);

glColor3f(0,1,0);
glVertex2f(-0.5,-0.5);

glColor3f(0,0,1);
glVertex2f(0.5,-0.5);

glEnd();
```

Conceptually:

```text
                 RED
                  ●
                 / \
                /   \
               /     \
              /       \
       GREEN ●---------● BLUE
```

Triangle-এর ভিতরের অংশে OpenGL color values **interpolate** করে, তাই মাঝখানে বিভিন্ন mixed color দেখা যায়।

---

# 14. `glColor3f()` কেন Vertex-এর আগে?

ধরো:

```cpp
glColor3f(1,0,0);
glVertex2f(0.0,0.5);
```

এখানে প্রথমে বলা হচ্ছে:

> এই Vertex-এর Color Red।

তারপর:

```cpp
glVertex2f(0.0,0.5);
```

দিয়ে Vertex-এর position দেওয়া হচ্ছে।

তাই সাধারণভাবে মনে রাখো:

```text
glColor3f()
     ↓
Color ঠিক করো

glVertex2f()
     ↓
Position দাও
```

---


# 15. Triangle-এর Position পরিবর্তন

Triangle-এর coordinate পরিবর্তন করলে পুরো Triangle-এর shape/position পরিবর্তন হবে।

### Example

```cpp
glVertex2f(0.0, 0.8);
glVertex2f(-0.8, -0.2);
glVertex2f(0.8, -0.2);
```

এতে Triangle আগের চেয়ে বড় হবে।

কারণ Pointগুলো Center থেকে আরও দূরে গেছে।

---

# 16. ছোট Triangle

```cpp
glVertex2f(0.0, 0.2);
glVertex2f(-0.2, -0.2);
glVertex2f(0.2, -0.2);
```

এতে Triangle ছোট হবে।

কারণ:

```text
Coordinate values ছোট
      ↓
Pointগুলো কাছাকাছি
      ↓
Triangle ছোট
```

---

# 17. Triangle-এর Direction বুঝি

আমাদের standard Triangle:

```cpp
glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);
```

Diagram:

```text
                 ●
                / \
               /   \
              /     \
             /       \
            ●---------●
```

এখানে:

```text
Top        → (0, 0.5)

Bottom Left  → (-0.5, -0.5)

Bottom Right → (0.5, -0.5)
```

---

# 18. Triangle-এর Vertex Order

এই code:

```cpp
glVertex2f(0.0,0.5);
glVertex2f(-0.5,-0.5);
glVertex2f(0.5,-0.5);
```

Vertexগুলো একটি নির্দিষ্ট order-এ দেওয়া হয়েছে।

```text
Vertex 1
   ↓
Vertex 2
   ↓
Vertex 3
   ↓
আবার Vertex 1
```

অর্থাৎ:

```text
1 → 2 → 3 → 1
```

এইভাবে Triangle-এর boundary তৈরি হয়।

Basic lab-এর জন্য সবচেয়ে important হলো:

> **৩টি coordinate দিলে OpenGL সেই ৩টি Vertex connect করে Triangle তৈরি করে।**

---

# 19. Multiple Triangle

`GL_TRIANGLES`-এ একসাথে একাধিক Triangle আঁকা যায়।

Rule:

```text
3 Vertex → 1 Triangle
6 Vertex → 2 Triangle
9 Vertex → 3 Triangle
```

অর্থাৎ:

```text
Number of Triangle = Number of Vertices ÷ 3
```

Example:

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(-0.8, 0.0);
glVertex2f(-0.5, 0.5);
glVertex2f(-0.2, 0.0);

glVertex2f(0.2, 0.0);
glVertex2f(0.5, 0.5);
glVertex2f(0.8, 0.0);

glEnd();
```

এখানে:

```text
6 Vertex
   ↓
6 ÷ 3
   ↓
2 Triangle
```

---
# 20. Triangle vs Line

| Line                | Triangle                |
| ------------------- | ----------------------- |
| `GL_LINES`          | `GL_TRIANGLES`          |
| 2 Vertex            | 3 Vertex                |
| 2 Point connect     | 3 Point connect         |
| `2 Vertex = 1 Line` | `3 Vertex = 1 Triangle` |

সহজভাবে:

```text
GL_LINES
2 Vertex → 1 Line

GL_TRIANGLES
3 Vertex → 1 Triangle
```

---
