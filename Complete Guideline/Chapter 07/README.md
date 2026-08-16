# Draw a Triangle

> OpenGL-এ ৩টি Vertex ব্যবহার করে একটি Triangle আঁকার basic method।

---

# 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* `GL_TRIANGLES` কী
* Triangle-এর জন্য কয়টি Vertex লাগে
* ৩টি coordinate কীভাবে Triangle তৈরি করে
* `glColor3f()` দিয়ে প্রতিটি Vertex-এর আলাদা Color দেওয়া
* Triangle-এর position পরিবর্তন করা

---

# 2. Basic Triangle Code

```cpp
glBegin(GL_TRIANGLES);

glVertex2f(0.0, 0.5);
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);

glEnd();
```

এখানে মোট **৩টি Vertex** আছে।

```text
3 Vertex → 1 Triangle
```

---

# 3. `glBegin(GL_TRIANGLES)`

```cpp
glBegin(GL_TRIANGLES);
```

OpenGL-কে বলা হচ্ছে:

> এখন আমরা **Triangle আঁকবো**।

এখানে:

```text
GL_TRIANGLES
      ↓
Triangle Drawing Mode
```

---

# 4. প্রথম Vertex

```cpp
glVertex2f(0.0, 0.5);
```

Coordinate:

```text
x = 0.0
y = 0.5
```

তাই Point হবে:

> **উপরে / Top**

```text
              ● (0,0.5)
```

---