# Draw a Circle

> OpenGL-এ `GL_POLYGON`, `for loop`, `sin()` এবং `cos()` ব্যবহার করে Circle-এর মতো smooth shape আঁকা।

---

# 1. Circle আঁকার Basic Idea

OpenGL-এ সহজভাবে সরাসরি:

```cpp
glBegin(GL_CIRCLE);
```

এরকম কোনো basic primitive নেই।

তাই আমরা অনেকগুলো ছোট ছোট point তৈরি করে সেগুলোকে `GL_POLYGON` দিয়ে connect করি।

```text
অনেকগুলো Point
      ↓
একটার পর একটা Connect
      ↓
GL_POLYGON
      ↓
Circle-এর মতো Shape
```

---

# 2. আমাদের Basic Circle Code

```cpp
glBegin(GL_POLYGON);

for(int i = 0; i < 360; i++)
{
    float angle = i * 3.1416 / 180.0;

    float x = -0.1 + 0.25 * cos(angle);
    float y =  0.0 + 0.25 * sin(angle);

    glVertex2f(x, y);
}

glEnd();
```

এখন একদম line by line বুঝি।

---

# 3. `glBegin(GL_POLYGON)`

```cpp
glBegin(GL_POLYGON);
```

এখানে OpenGL-কে বলছি:

> আমরা এখন একটি Polygon আঁকবো।

কিন্তু এখানে একটা প্রশ্ন আসবে:

**Circle-এর জন্য Polygon কেন?**

কারণ আমরা অনেকগুলো Vertex তৈরি করবো।

```text
অনেক Vertex
     ↓
অনেক ছোট ছোট Line
     ↓
প্রায় গোল Shape
```

Vertex যত বেশি হবে, shape তত smooth দেখাবে।

---

# 4. `for` Loop

```cpp
for(int i = 0; i < 360; i++)
```

এটাই Circle code-এর সবচেয়ে important অংশ।

এখানে:

```text
i = 0
```

দিয়ে শুরু হচ্ছে।

তারপর:

```text
i < 360
```

যতক্ষণ true, loop চলবে।

প্রতিবার:

```text
i++
```

হবে।

অর্থাৎ:

```text
0
1
2
3
4
...
358
359
```

তারপর `i = 360` হলে:

```text
360 < 360
```

False।

তখন loop শেষ।

---

# 5. 360 কেন?

কারণ একটি full circle:

```text
360°
```

তাই আমরা:

```cpp
for(int i = 0; i < 360; i++)
```

দিয়ে পুরো circle-এর চারপাশে ঘুরছি।

```text
0° → 360°
```

সহজভাবে:

> **360 degree ঘুরে Circle complete করছি।**

---

# 6. `float angle`

```cpp
float angle = i * 3.1416 / 180.0;
```

এই line-টা প্রথমে একটু কঠিন মনে হতে পারে।

এখানে আমরা `i`-কে **degree থেকে radian-এ convert** করছি।

কারণ C/C++ এর:

```cpp
sin()
cos()
```

সাধারণভাবে angle **radian** হিসেবে নেয়।

---

# 7. Degree থেকে Radian

Formula:

```text
Radian = Degree × π / 180
```

আমাদের code:

```cpp
float angle = i * 3.1416 / 180.0;
```

এখানে:

```text
i → Degree

3.1416 → π-এর কাছাকাছি value

180 → Degree to Radian conversion
```

---

# 8. Example

যদি:

```text
i = 0
```

তাহলে:

```text
angle = 0 × 3.1416 / 180
      = 0
```

যদি:

```text
i = 90
```

তাহলে:

```text
angle = 90 × 3.1416 / 180
      ≈ 1.57
```

যদি:

```text
i = 180
```

তাহলে:

```text
angle ≈ 3.14
```

যদি:

```text
i = 360
```

তাহলে:

```text
angle ≈ 6.28
```

অর্থাৎ:

```text
0° → 0 radian

90° → π/2

180° → π

360° → 2π
```

---

# 9. `x` Coordinate

এখন আসি:

```cpp
float x = -0.1 + 0.25 * cos(angle);
```

এখানে Circle-এর প্রতিটি point-এর **X coordinate** বের করছি।

Basic formula:

```text
x = centerX + radius × cos(angle)
```

আমাদের code-এ:

```text
centerX = -0.1
radius  = 0.25
```

তাই:

```cpp
x = -0.1 + 0.25 * cos(angle);
```

---

# 10. `-0.1` কেন?

```cpp
float x = -0.1 + 0.25 * cos(angle);
```

এখানে:

```text
-0.1
```

হলো Circle-এর **Center X**।

অর্থাৎ Circle-এর center:

```text
X = -0.1
```

তাই Circle center থেকে একটু **left side**-এ থাকবে।

---

# 11. `0.25` কেন?

```cpp
0.25 * cos(angle)
```

এখানে:

```text
0.25 = Radius
```

অর্থাৎ Circle-এর center থেকে edge পর্যন্ত distance:

```text
0.25
```

Diagram:

```text
Center ●────────● Edge
       ← 0.25 →
```

তাই:

> `0.25` হলো Circle-এর size control করার value।

---

# 12. Radius Change করা যায়?

অবশ্যই।

বর্তমানে:

```cpp
0.25
```

আছে।

চাইলে:

```cpp
0.4
```

দিতে পারো।

```cpp
float x = -0.1 + 0.4 * cos(angle);
float y =  0.0 + 0.4 * sin(angle);
```

তাহলে Circle বড় হবে।

আর:

```cpp
0.1
```

দিলে ছোট হবে।

```text
Radius বড়
   ↓
Circle বড়

Radius ছোট
   ↓
Circle ছোট
```

---

# 13. `y` Coordinate

এখন:

```cpp
float y = 0.0 + 0.25 * sin(angle);
```

এখানে Circle-এর প্রতিটি point-এর **Y coordinate** বের করছি।

Basic formula:

```text
y = centerY + radius × sin(angle)
```

আমাদের code:

```text
centerY = 0.0
radius  = 0.25
```

তাই:

```cpp
y = 0.0 + 0.25 * sin(angle);
```

---

# 14. `0.0` কেন?

```cpp
float y = 0.0 + 0.25 * sin(angle);
```

এখানে:

```text
0.0
```

হলো Circle-এর **Center Y**।

অর্থাৎ:

```text
Center X = -0.1
Center Y = 0.0
```

তাই Circle-এর center:

```text
(-0.1, 0.0)
```

---

# 15. `cos()` কী করছে?

```cpp
cos(angle)
```

Circle-এর point-এর **X direction** determine করতে সাহায্য করছে।

মনে রাখো:

```text
cos()
 ↓
X
```

তাই:

```cpp
x = centerX + radius * cos(angle);
```

---

# 16. `sin()` কী করছে?

```cpp
sin(angle)
```

Circle-এর point-এর **Y direction** determine করতে সাহায্য করছে।

মনে রাখো:

```text
sin()
 ↓
Y
```

তাই:

```cpp
y = centerY + radius * sin(angle);
```

---

# 17. সবচেয়ে Important Formula

Circle-এর point বের করার formula:

```text
x = centerX + radius × cos(angle)

y = centerY + radius × sin(angle)
```

Code:

```cpp
float x = centerX + radius * cos(angle);
float y = centerY + radius * sin(angle);
```

এই formula-টাই **মুখস্থ করে ফেলো**।

---

# 18. `glVertex2f(x,y)`

এখন:

```cpp
glVertex2f(x, y);
```

এর কাজ হলো:

> আমরা যে X এবং Y coordinate calculate করেছি, সেই position-এ একটি Vertex বসানো।

অর্থাৎ:

```text
x → কোথায় horizontally?

y → কোথায় vertically?
```

এই দুইটা মিলে:

```text
(x,y) → একটি Point/Vertex
```

---

# 19. Loop-এর ভিতরে কেন `glVertex2f()`?

কারণ আমরা শুধু একটি point চাই না।

আমরা চাই:

```text
0°
1°
2°
3°
...
359°
```

প্রতিটি angle-এর জন্য একটি করে point।

তাই:

```cpp
for(...)
{
    calculate x;
    calculate y;
    glVertex2f(x,y);
}
```

মানে:

```text
Angle
 ↓
X,Y Calculate
 ↓
Vertex
 ↓
Next Angle
 ↓
X,Y Calculate
 ↓
Vertex
 ↓
...
```

---