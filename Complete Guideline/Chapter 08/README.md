# Draw a Rectangle

> OpenGL-এ ৪টি Vertex ব্যবহার করে একটি Rectangle আঁকার basic method।

---

# 1. কী শিখবো?

এই file থেকে আমরা শিখবো:

* `GL_QUADS` কী
* Rectangle-এর জন্য কয়টি Vertex লাগে
* ৪টি coordinate কীভাবে Rectangle তৈরি করে
* Vertex-এর order কেন important
* Rectangle-এর position ও size কীভাবে change করতে হয়
* Rectangle-এর color কীভাবে দিতে হয়

---
# 2. Basic Rectangle Code

```cpp
glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

এখানে মোট **৪টি Vertex** আছে।

```text
4 Vertex → 1 Rectangle
```

---