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