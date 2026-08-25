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
