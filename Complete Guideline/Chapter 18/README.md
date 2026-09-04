# Draw a House

> OpenGL-এ basic shapes একসাথে ব্যবহার করে একটি simple House আঁকা।

---

# 1. House কীভাবে বানাবো?

একটা simple House-কে কয়েকটা অংশে ভাগ করবো:

```text
       /\
      /  \        ← Roof (Triangle)
     /____\
     |    |
     | [] |       ← Window
     |    |
     | __ |
     ||  ||       ← Door
     |____|
```

আমরা ব্যবহার করবো:

```text
House Body → GL_QUADS
Roof       → GL_TRIANGLES
Door       → GL_QUADS
Window     → GL_QUADS
```

অর্থাৎ:

```text
Basic Shapes
     ↓
Combine
     ↓
House
```

---
