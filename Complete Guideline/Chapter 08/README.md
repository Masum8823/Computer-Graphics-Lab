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

# 7. চতুর্থ Vertex

```cpp
glVertex2f(-0.5, -0.5);
```

এখানে:

```text
x = -0.5 → Left
y = -0.5 → Down
```

তাই এটি:

> **Bottom Left**

শেষে পুরো shape হবে:

```text
        (-0.5,0.5) ●────────────● (0.5,0.5)
                   |              |
                   |              |
                   |              |
        (-0.5,-0.5)●────────────● (0.5,-0.5)
```

---

# 8. চারটি Vertex কীভাবে Rectangle হলো?

আমাদের চারটি Vertex:

```text
1 → (-0.5,  0.5)  Top Left

2 → ( 0.5,  0.5)  Top Right

3 → ( 0.5, -0.5)  Bottom Right

4 → (-0.5, -0.5)  Bottom Left
```

OpenGL এগুলোকে order অনুযায়ী connect করে:

```text
1 → 2
2 → 3
3 → 4
4 → 1
```

তাই Rectangle তৈরি হয়।

---

# 9. Vertex Order খুব Important

আমাদের code:

```cpp
glVertex2f(-0.5, 0.5);   // 1
glVertex2f(0.5, 0.5);    // 2
glVertex2f(0.5, -0.5);   // 3
glVertex2f(-0.5, -0.5);  // 4
```

এটা basically:

```text
1 → 2 → 3 → 4 → 1
```

অর্থাৎ এক পাশ থেকে শুরু করে চারপাশ ঘুরে আসছি।

### সহজভাবে মনে রাখো

> **Top Left → Top Right → Bottom Right → Bottom Left**

এটা Rectangle-এর জন্য খুব easy sequence।

---

# 10. কেন সরাসরি ১ থেকে ৩ এ যাওয়া যাবে না?

Rectangle-এর চারপাশ follow করতে হবে।

সঠিক:

```text
1 → 2 → 3 → 4 → 1
```

ভুলভাবে:

```text
1 → 3 → 2 → 4
```

দিলে shape-এর vertex order এলোমেলো হয়ে যেতে পারে।

তাই basic lab-এর জন্য সবসময় চারপাশ ঘুরে coordinate দাও।

---