# Colors in OpenGL

> OpenGL-এ কোনো Point, Line, Triangle, Rectangle বা অন্য Shape-এর Color দেওয়ার জন্য `glColor3f()` ব্যবহার করা হয়।

---

# 1. কী শিখবো?

এই file থেকে আমরা শিখবো:

* `glColor3f()` কী
* RGB কী
* `glColor3f()`-এর 3টি value কী বোঝায়
* Red, Green, Blue কীভাবে তৈরি হয়
* এক Shape-এর এক Color
* একই Shape-এর বিভিন্ন Vertex-এ বিভিন্ন Color
* Color কখন দিতে হবে

---

# 2. `glColor3f()` কী?

OpenGL-এ Color দেওয়ার জন্য:

```cpp
glColor3f(R, G, B);
```

ব্যবহার করা হয়।

এখানে:

```text id="j0n9ac"
R → Red
G → Green
B → Blue
```

অর্থাৎ:

```text id="3s5czi"
glColor3f(R, G, B)
             ↓
         RGB Color
```

---

# 3. RGB কী?

RGB মানে:

```text id="4x5n9k"
R = Red
G = Green
B = Blue
```

এই তিনটি basic color মিশিয়ে বিভিন্ন color তৈরি করা যায়।

প্রতিটি value সাধারণত:

```text id="t8r8lq"
0.0 → Minimum
1.0 → Maximum
```

---

# 4. Red Color

```cpp id="3s8n1x"
glColor3f(1.0, 0.0, 0.0);
```

এখানে:

```text id="9b3zlo"
R = 1 → Full Red
G = 0 → No Green
B = 0 → No Blue
```

তাই:

> **Red**

সহজভাবে:

```text id="rflm70"
(1,0,0) → Red
```

---

# 5. Green Color

```cpp id="7qk8dr"
glColor3f(0.0, 1.0, 0.0);
```

এখানে:

```text id="0q3tqj"
R = 0
G = 1
B = 0
```

তাই:

> **Green**

মনে রাখো:

```text id="1v8npu"
(0,1,0) → Green
```

---

# 6. Blue Color

```cpp id="5g7u2z"
glColor3f(0.0, 0.0, 1.0);
```

এখানে:

```text id="h0y0kv"
R = 0
G = 0
B = 1
```

তাই:

> **Blue**

```text id="q3wq4m"
(0,0,1) → Blue
```

---

# 7. Black Color

```cpp id="n9k2jf"
glColor3f(0.0, 0.0, 0.0);
```

সবগুলো value 0:

```text id="q4t2uj"
R = 0
G = 0
B = 0
```

তাই:

> **Black**

```text id="8p3u1h"
(0,0,0) → Black
```

---

# 8. White Color

```cpp id="9a7e3q"
glColor3f(1.0, 1.0, 1.0);
```

সবগুলো value maximum:

```text id="3u6d1g"
R = 1
G = 1
B = 1
```

তাই:

> **White**

```text id="u4nq0z"
(1,1,1) → White
```

---

# 9. Yellow Color

Yellow বানাতে:

```cpp id="7j7p4k"
glColor3f(1.0, 1.0, 0.0);
```

মানে:

```text id="w9x9w8"
R = 1
G = 1
B = 0
```

Red + Green:

```text id="0wqjvq"
Red + Green → Yellow
```

তাই:

```text id="xw9p0q"
(1,1,0) → Yellow
```

---

# 10. Cyan Color

```cpp id="3e4g8p"
glColor3f(0.0, 1.0, 1.0);
```

মানে:

```text id="y8b0kg"
R = 0
G = 1
B = 1
```

Green + Blue:

```text id="q1p5sd"
Green + Blue → Cyan
```

তাই:

```text id="c0p6v2"
(0,1,1) → Cyan
```

---

# 11. Magenta Color

```cpp id="2ap4qn"
glColor3f(1.0, 0.0, 1.0);
```

মানে:

```text id="c2z5kn"
R = 1
G = 0
B = 1
```

Red + Blue:

```text id="p1ly9h"
Red + Blue → Magenta
```

তাই:

```text id="6ck2nt"
(1,0,1) → Magenta
```

---

# 12. Important Basic Colors

| Color   |  R |  G |  B |
| ------- | -: | -: | -: |
| Black   |  0 |  0 |  0 |
| Red     |  1 |  0 |  0 |
| Green   |  0 |  1 |  0 |
| Blue    |  0 |  0 |  1 |
| White   |  1 |  1 |  1 |
| Yellow  |  1 |  1 |  0 |
| Cyan    |  0 |  1 |  1 |
| Magenta |  1 |  0 |  1 |

এই table-টা lab-এর জন্য **মুখস্থ করে ফেললে ভালো**।

---

# 13. `glColor3f()`-এ Value Range

সাধারণভাবে:

```text id="9x4bqk"
0.0 → Minimum
1.0 → Maximum
```

তাই:

```cpp id="n0a4tc"
glColor3f(1.0, 0.0, 0.0);
```

মানে Full Red।

আবার:

```cpp id="d2k6cd"
glColor3f(0.5, 0.0, 0.0);
```

মানে Red-এর intensity কম।

---

# 14. `0.5` কেন ব্যবহার করবো?

ধরো:

```cpp id="3c7xvs"
glColor3f(0.5, 0.0, 0.0);
```

এখানে:

```text id="l2s0h8"
Red = 0.5
```

অর্থাৎ Red-এর intensity `1.0` থেকে কম।

একইভাবে:

```cpp id="q1d1bs"
glColor3f(0.0, 0.5, 0.0);
```

→ Darker Green

```cpp id="q6g6o0"
glColor3f(0.0, 0.0, 0.5);
```

→ Darker Blue

---
# 15. Color + Point

আগে আমরা Point এভাবে এঁকেছিলাম:

```cpp id="zldh6c"
glPointSize(10);

glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);

glEnd();
```

এখন Color যোগ করি:

```cpp id="y2y0f0"
glPointSize(10);

glColor3f(1.0, 0.0, 0.0);

glBegin(GL_POINTS);

glVertex2f(0.0, 0.0);

glEnd();
```

এখানে Point হবে:

> **Red**

---

# 16. Color + Line

```cpp id="5e1r9f"
glColor3f(0.0, 1.0, 0.0);

glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

এখানে Line হবে:

> **Green**

---

# 17. Color + Triangle

```cpp id="9a1r8w"
glColor3f(0.0, 0.0, 1.0);

glBegin(GL_TRIANGLES);

glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এখানে পুরো Triangle হবে:

> **Blue**

---

# 18. Color + Rectangle

```cpp id="08g9qf"
glColor3f(1.0, 1.0, 0.0);

glBegin(GL_QUADS);

glVertex2f(-0.5, 0.5);
glVertex2f(0.5, 0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, -0.5);

glEnd();
```

এখানে Rectangle হবে:

> **Yellow**

---

# 19. Color + Polygon

```cpp id="e0e9su"
glColor3f(1.0, 0.0, 1.0);

glBegin(GL_POLYGON);

glVertex2f(0.0, 0.7);
glVertex2f(0.6, 0.3);
glVertex2f(0.4, -0.5);
glVertex2f(-0.4, -0.5);
glVertex2f(-0.6, 0.3);

glEnd();
```

এখানে Polygon হবে:

> **Magenta**

---

# 20. সবচেয়ে Important: `glColor3f()` কোথায় লিখবো?

Basic code-এ সহজভাবে:

```cpp id="1v4kz1"
glColor3f(1.0, 0.0, 0.0);

glBegin(GL_TRIANGLES);

glVertex2f(0.0,0.5);
glVertex2f(-0.5,-0.5);
glVertex2f(0.5,-0.5);

glEnd();
```

এখানে:

```text id="y0l8ko"
glColor3f()
    ↓
Color Set

glBegin()
    ↓
Shape Start

glVertex2f()
    ↓
Shape Draw
```

অর্থাৎ:

> **Shape আঁকার আগে Color set করে দিলে পুরো shape সেই color হবে।**

---

# 21. এক Shape-এ Multiple Color

এটাই Triangle-এর ক্ষেত্রে আমরা করেছিলাম।

```cpp id="l0v4ps"
glBegin(GL_TRIANGLES);

glColor3f(1,0,0);
glVertex2f(0.0,0.5);

glColor3f(0,1,0);
glVertex2f(-0.5,-0.5);

glColor3f(0,0,1);
glVertex2f(0.5,-0.5);

glEnd();
```

এখানে:

```text id="h4a4ha"
Vertex 1 → Red
Vertex 2 → Green
Vertex 3 → Blue
```

OpenGL মাঝের অংশে color interpolate করতে পারে।

তাই Triangle-এর ভিতরে বিভিন্ন mixed color দেখা যাবে।

---

# 22. `glColor3f()` + `glVertex2f()` Relationship

এই দুইটা খুব ভালোভাবে মনে রাখো:

```cpp id="1y0mqp"
glColor3f(1,0,0);
glVertex2f(0.0,0.5);
```

প্রথম Line:

```text id="76l4cv"
Color → Red
```

দ্বিতীয় Line:

```text id="bq3xv7"
Position → (0.0,0.5)
```

অর্থাৎ:

```text id="0v1v9k"
glColor3f()
      ↓
WHAT COLOR?

glVertex2f()
      ↓
WHERE?
```

---

# 23. RGB মনে রাখার সহজ Trick

`glColor3f(R,G,B)`-এ order সবসময়:

```text id="oz8q5x"
R → G → B
```

অর্থাৎ:

```text id="y9e6n8"
1st → Red
2nd → Green
3rd → Blue
```

Example:

```cpp id="ypa6qt"
glColor3f(1, 0, 0);
```

প্রথম value `1` → Red।

```cpp id="ahh1sp"
glColor3f(0, 1, 0);
```

দ্বিতীয় value `1` → Green।

```cpp id="k21gse"
glColor3f(0, 0, 1);
```

তৃতীয় value `1` → Blue।

---

# 24. Background Color vs Shape Color

এখানে একটা important difference আছে।

### Background Color

```cpp id="9l6w6r"
glClearColor(0.0, 0.0, 0.0, 1.0);
```

এটা:

> Window-এর **background color** সেট করে।

---

### Shape Color

```cpp id="s7d9fq"
glColor3f(1.0, 0.0, 0.0);
```

এটা:

> Shape-এর **color** সেট করে।

তাই:

```text id="ck8cxj"
glClearColor()
      ↓
Background

glColor3f()
      ↓
Object/Shape
```

এটা exam-এর জন্য important difference।

---