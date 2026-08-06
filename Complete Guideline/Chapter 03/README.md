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

# 3. OpenGL Coordinate System

Basic OpenGL coordinate system সাধারণভাবে এমন:

```text
                       +Y
                        ↑
                        |
                        |
                        |
              (-)       |       (+)
                        |
          -X  ←---------+---------→  +X
                       (0,0)
                        |
                        |
                        |
                        ↓
                       -Y
```

এখানে Screen-এর Center:

```text
(0,0)
```

---

# 4. `(0,0)` কী?

```cpp
glVertex2f(0.0, 0.0);
```

এখানে:

```text
x = 0
y = 0
```

এটি হলো Coordinate System-এর **Origin**।

সহজভাবে:

> `(0,0)` = Center

```text
+---------------------------+
|                           |
|                           |
|            (0,0)          |
|              ●            |
|                           |
|                           |
+---------------------------+
```

---

# 5. X-Axis

X-axis হলো **Horizontal Line**।

```text
        -X              0              +X
         ←--------------|--------------→
                        |
```

### X-এর value:

```text
Negative X → Left

Positive X → Right
```

উদাহরণ:

```cpp
glVertex2f(-0.5, 0.0);
```

Point হবে Center-এর **বাম দিকে**।

আর:

```cpp
glVertex2f(0.5, 0.0);
```

Point হবে Center-এর **ডান দিকে**।

---

# 6. Y-Axis

Y-axis হলো **Vertical Line**।

```text
                       +Y
                        ↑
                        |
                        |
                        0
                        |
                        |
                        ↓
                       -Y
```

### Y-এর value:

```text
Positive Y → Up

Negative Y → Down
```

উদাহরণ:

```cpp
glVertex2f(0.0, 0.5);
```

Point হবে Center-এর **উপরে**।

আর:

```cpp
glVertex2f(0.0, -0.5);
```

Point হবে Center-এর **নিচে**।

---
