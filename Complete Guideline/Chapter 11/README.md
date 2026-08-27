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