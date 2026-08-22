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
