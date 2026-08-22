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