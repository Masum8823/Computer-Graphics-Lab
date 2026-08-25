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