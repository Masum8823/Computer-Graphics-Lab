# Draw an Ellipse

> Ellipse হলো Circle-এর মতো একটি গোলাকার shape, কিন্তু একদিকে বেশি লম্বা এবং অন্যদিকে তুলনামূলক ছোট।

---

# 1. Ellipse কী?

Circle:

```text
Width = Height
```

Ellipse:

```text
Width ≠ Height
```

সহজভাবে:

```text
Circle:

      ****
   **      **
  *          *
   **      **
      ****


Ellipse:

       ******
    **        **
  **            **
    **        **
       ******
```

---

# 2. Circle-এর সাথে Ellipse-এর সম্পর্ক

Circle-এর formula ছিল:

```cpp
x = centerX + radius * cos(angle);
y = centerY + radius * sin(angle);
```

Ellipse-এর ক্ষেত্রে আমরা **X radius** এবং **Y radius** আলাদা করে দিই।

```cpp
x = centerX + radiusX * cos(angle);
y = centerY + radiusY * sin(angle);
```

এটাই সবচেয়ে important difference।

---

# 3. Basic Ellipse Code

```cpp
glBegin(GL_POLYGON);

for(int i = 0; i < 360; i++)
{
    float angle = i * 3.1416 / 180.0;

    float x = 0.0 + 0.6 * cos(angle);
    float y = 0.0 + 0.3 * sin(angle);

    glVertex2f(x, y);
}

glEnd();
```

এখন line by line বুঝি।

---


# 4. `glBegin(GL_POLYGON)`

```cpp
glBegin(GL_POLYGON);
```

এখানে OpenGL-কে বলছি:

> আমরা Polygon drawing শুরু করছি।

Circle-এর মতো এখানেও অনেকগুলো Vertex তৈরি করবো।

```text
Many Vertex
     ↓
GL_POLYGON
     ↓
Ellipse Shape
```

---

# 5. `for` Loop

```cpp
for(int i = 0; i < 360; i++)
```

এখানে:

```text
i = 0
```

দিয়ে শুরু হবে।

তারপর:

```text
0
1
2
3
...
359
```

পর্যন্ত চলবে।

কারণ:

```text
Full Circle = 360°
```

Ellipse-এর ক্ষেত্রেও আমরা পুরো 360° ঘুরে point তৈরি করি।

---

# 6. `angle` তৈরি

```cpp
float angle = i * 3.1416 / 180.0;
```

এখানে degree-কে radian-এ convert করছি।

কারণ:

```cpp
sin()
cos()
```

এর জন্য angle radian-এ ব্যবহার করা হয়।

Formula:

```text
Radian = Degree × π / 180
```

তাই:

```cpp
i * 3.1416 / 180.0
```

---

# 7. X Coordinate

```cpp
float x = 0.0 + 0.6 * cos(angle);
```

এখানে:

```text
0.0 → Center X

0.6 → X Radius
```

অর্থাৎ:

```text
x = centerX + radiusX × cos(angle)
```

আমাদের:

```text
centerX = 0.0
radiusX = 0.6
```

---

# 8. Y Coordinate

```cpp
float y = 0.0 + 0.3 * sin(angle);
```

এখানে:

```text
0.0 → Center Y

0.3 → Y Radius
```

অর্থাৎ:

```text
y = centerY + radiusY × sin(angle)
```

আমাদের:

```text
centerY = 0.0
radiusY = 0.3
```

---

# 9. সবচেয়ে Important Difference

Circle:

```cpp
x = centerX + 0.25 * cos(angle);
y = centerY + 0.25 * sin(angle);
```

এখানে:

```text
X Radius = 0.25
Y Radius = 0.25
```

দুটো equal।

তাই:

```text
Circle
```

---

Ellipse:

```cpp
x = centerX + 0.6 * cos(angle);
y = centerY + 0.3 * sin(angle);
```

এখানে:

```text
X Radius = 0.6
Y Radius = 0.3
```

দুটো different।

তাই:

```text
Ellipse
```

---

# 10. `0.6` কেন?

```cpp
0.6 * cos(angle)
```

এখানে:

```text
0.6 = X Radius
```

অর্থাৎ Ellipse কতটা **left-right** দিকে বড় হবে সেটা control করে।

```text
X Radius বাড়ালে
       ↓
Ellipse বেশি চওড়া হবে
```

---

# 11. `0.3` কেন?

```cpp
0.3 * sin(angle)
```

এখানে:

```text
0.3 = Y Radius
```

এটা Ellipse-এর **up-down** size control করে।

```text
Y Radius বাড়ালে
       ↓
Ellipse বেশি লম্বা হবে
```

---

# 12. `0.6` এবং `0.3` কি Fixed?

না।

এগুলো শুধু example।

চাইলে:

```cpp
x = 0.0 + 0.8 * cos(angle);
y = 0.0 + 0.4 * sin(angle);
```

দিতে পারো।

তাহলে:

```text
X Radius = 0.8
Y Radius = 0.4
```

Ellipse আরও বড় হবে।

---

# 13. Radius X vs Radius Y

এটা খুব ভালোভাবে মনে রাখবে:

```text
radiusX
   ↓
Left ↔ Right
```

আর:

```text
radiusY
   ↓
Up ↕ Down
```

Diagram:

```text
              Y
              ↑
              |
        .------------.
      .'              '.
     /                  \
----●---------+----------●----→ X
     \        |         /
      '.      |       .'
        '------------'

    ←── radiusX ──→
          ↑
       radiusY
```

---

# 14. `glVertex2f(x,y)`

```cpp
glVertex2f(x, y);
```

এখানে calculated X এবং Y coordinate ব্যবহার করে একটি Vertex তৈরি হচ্ছে।

```text
x → Horizontal position
y → Vertical position
```

তাই:

```text
(x,y)
  ↓
Vertex
```

---

# 15. কেন Loop-এর ভিতরে `glVertex2f()`?

কারণ প্রতিটি angle-এর জন্য আলাদা point দরকার।

```text
i = 0
 ↓
Point

i = 1
 ↓
Point

i = 2
 ↓
Point

...

i = 359
 ↓
Point
```

সব point:

```text
GL_POLYGON
     ↓
Connect
     ↓
Ellipse
```

---

# 16. `glEnd()`

```cpp
glEnd();
```

এর মাধ্যমে Polygon drawing শেষ হচ্ছে।

পুরো flow:

```text
glBegin(GL_POLYGON)
        ↓
for loop
        ↓
angle
        ↓
x,y calculate
        ↓
glVertex2f()
        ↓
glEnd()
```

---

# 17. Ellipse-এর Center

আমাদের code:

```cpp
float x = 0.0 + 0.6 * cos(angle);
float y = 0.0 + 0.3 * sin(angle);
```

এখানে:

```text
Center X = 0.0
Center Y = 0.0
```

তাই:

```text
Center = (0.0, 0.0)
```

---

# 18. Ellipse-এর Position Change

ধরো:

```cpp
float x = 0.3 + 0.6 * cos(angle);
float y = 0.2 + 0.3 * sin(angle);
```

এখন:

```text
Center = (0.3, 0.2)
```

তাই Ellipse:

```text
Right → 0.3
Up    → 0.2
```

দিকে move করবে।

মনে রাখবে:

```text
centerX → Left/Right position
centerY → Up/Down position
```

---


# 19. Ellipse-এর Size Change

ধরো:

```cpp
float x = 0.0 + 0.8 * cos(angle);
float y = 0.0 + 0.4 * sin(angle);
```

এখানে:

```text
X Radius = 0.8
Y Radius = 0.4
```

তাই Ellipse বড় হবে।

---

# 20. Width এবং Height

Ellipse-এর approximately:

```text
Width  = 2 × radiusX
Height = 2 × radiusY
```

আমাদের example:

```text
radiusX = 0.6
radiusY = 0.3
```

তাই:

```text
Width  = 2 × 0.6 = 1.2

Height = 2 × 0.3 = 0.6
```

---


# 21. Circle কখন হবে?

যদি:

```text
radiusX = radiusY
```

হয়, তাহলে Ellipse আর Ellipse থাকবে না—Circle হয়ে যাবে।

যেমন:

```cpp
x = 0.0 + 0.4 * cos(angle);
y = 0.0 + 0.4 * sin(angle);
```

এখানে:

```text
X Radius = 0.4
Y Radius = 0.4
```

তাই:

```text
Circle
```

---

# 22. সহজ Rule

```text
radiusX = radiusY
        ↓
      Circle
```

আর:

```text
radiusX ≠ radiusY
        ↓
     Ellipse
```

এটা খুব important।

---

# 23. Horizontal Ellipse

```cpp
float x = 0.0 + 0.7 * cos(angle);
float y = 0.0 + 0.3 * sin(angle);
```

এখানে:

```text
X Radius = 0.7
Y Radius = 0.3
```

তাই:

```text
Width বেশি
Height কম
```

এটি horizontal ellipse।

```text
     __________
   /            \
  /              \
  \              /
   \____________/
```

---
