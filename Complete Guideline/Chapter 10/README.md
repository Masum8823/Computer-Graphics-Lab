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