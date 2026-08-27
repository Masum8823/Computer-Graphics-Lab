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