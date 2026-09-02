# Draw a Star

> OpenGL-এ কয়েকটি Vertex নির্দিষ্টভাবে বসিয়ে এবং `GL_POLYGON` ব্যবহার করে একটি simple 5-point Star আঁকা।

---

# 1. Star কীভাবে আঁকবো?

আমরা একটা 5-point Star বানাতে **10টা Vertex** ব্যবহার করবো।

কেন 10টা?

```text
5টা Outer Point
+
5টা Inner Point
=
10টা Vertex
```

সহজভাবে:

```text
        Outer
          ●
         / \
        /   \
   ●---●     ●---●
    \           /
     ●         ●
      \       /
       ●-----●
```

আসলে আমরা Outer আর Inner point একটার পর একটা দেবো।

---