# OpenGL 2D Coordinate System

> OpenGL-এ কোনো Point বা Shape কোথায় আঁকতে হবে সেটা Coordinate দিয়ে নির্ধারণ করা হয়।

---

## 1. কী শিখবো?

এই file-এ আমরা শিখবো:

* Coordinate System কী
* `(x, y)` কী
* `(0, 0)` কোথায়
* `x` এবং `y` কীভাবে কাজ করে
* Positive ও Negative Coordinate
* `glVertex2f(x, y)` কীভাবে বুঝবো
* Point কোথায় হবে সেটা দ্রুত বের করার Trick

---

# 2. Coordinate System কী?

Coordinate System ব্যবহার করে Screen-এর কোনো নির্দিষ্ট জায়গা চিহ্নিত করা হয়।

OpenGL-এর 2D drawing-এ আমরা সাধারণত:

```cpp
glVertex2f(x, y);
```

ব্যবহার করি।

এখানে:

```text
x → Horizontal Position
y → Vertical Position
```

অর্থাৎ:

> `x` বলে Point কতটা **বামে বা ডানে** যাবে।

> `y` বলে Point কতটা **উপরে বা নিচে** যাবে।

---