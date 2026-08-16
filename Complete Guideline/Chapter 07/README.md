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
