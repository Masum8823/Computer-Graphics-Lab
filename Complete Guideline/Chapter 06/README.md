# Draw a Line

> OpenGL-এ দুটি Point/Vertex-এর মধ্যে একটি straight line আঁকার basic method।

---

## 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* `GL_LINES` কী
* Line আঁকার জন্য কয়টি coordinate লাগে
* `glVertex2f()` কীভাবে Line-এর starting ও ending point দেয়
* Horizontal, Vertical ও Diagonal Line
* Line-এর color পরিবর্তন
* একাধিক Line আঁকার basic rule

---

# 2. Basic Code

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

এটাই আমাদের মূল Line drawing code।

---
