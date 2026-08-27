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