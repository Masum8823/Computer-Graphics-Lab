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
