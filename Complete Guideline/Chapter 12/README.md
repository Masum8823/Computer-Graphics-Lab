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