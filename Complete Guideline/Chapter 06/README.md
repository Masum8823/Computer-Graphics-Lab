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

# 3. Line কীভাবে তৈরি হলো?

এখানে দুইটি Vertex দেওয়া হয়েছে:

```cpp
glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);
```

প্রথম Point:

```text
(-0.5, 0.0)
```

দ্বিতীয় Point:

```text
(0.5, 0.0)
```

OpenGL এই দুইটি Point-এর মধ্যে সরাসরি একটি straight line তৈরি করে।

```text
(-0.5,0) ●──────────────● (0.5,0)
```

---

# 4. `glBegin(GL_LINES)`

```cpp
glBegin(GL_LINES);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Line আঁকবো**।

এখানে:

```text
GL_LINES
   ↓
Line Drawing Mode
```

---

# 5. `glVertex2f()` দিয়ে দুইটি Point

### First Point

```cpp
glVertex2f(-0.5, 0.0);
```

এটি Line-এর **starting point**।

```text
X = -0.5 → Left
Y =  0.0 → Center level
```

তাই Point টি Center-এর বাম দিকে।

---

### Second Point

```cpp
glVertex2f(0.5, 0.0);
```

এটি Line-এর **ending point**।

```text
X = 0.5 → Right
Y = 0.0 → Center level
```

তাই Point টি Center-এর ডান দিকে।

---

# 6. কেন দুইটি Point লাগে?

Line হলো দুইটি Point-এর মধ্যে একটি straight connection।

তাই:

```text
Point 1 ───────── Point 2
```

এর জন্য minimum দুইটি vertex লাগে।

```cpp
glVertex2f(x1, y1);
glVertex2f(x2, y2);
```

এখানে:

```text
(x1,y1) → Starting Point
(x2,y2) → Ending Point
```

---
