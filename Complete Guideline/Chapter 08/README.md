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

# 3. `glBegin(GL_QUADS)`

```cpp
glBegin(GL_QUADS);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Quadrilateral/Quad** আঁকবো।

`GL_QUADS`-এ সাধারণভাবে **৪টি Vertex** মিলে একটি four-sided shape তৈরি করে।

```text
GL_QUADS
   ↓
4 Vertex
   ↓
1 Quad
```

আমাদের Rectangle হলো একটি Quad।

---

# 4. প্রথম Vertex

```cpp
glVertex2f(-0.5, 0.5);
```

Coordinate:

```text
x = -0.5 → Left
y =  0.5 → Up
```

তাই এটি:

> **Top Left**

```text
● (-0.5,0.5)
```

---

# 5. দ্বিতীয় Vertex

```cpp
glVertex2f(0.5, 0.5);
```

এখানে:

```text
x = 0.5 → Right
y = 0.5 → Up
```

তাই এটি:

> **Top Right**

```text
(-0.5,0.5) ●────────● (0.5,0.5)
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

তাই এটি:

> **Bottom Right**

```text
(-0.5,0.5) ●────────● (0.5,0.5)
                         |
                         |
                         ● (0.5,-0.5)
```

---