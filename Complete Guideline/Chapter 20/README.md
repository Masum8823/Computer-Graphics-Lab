# Rotation

> Rotation হলো কোনো object/shape-কে একটি নির্দিষ্ট **angle** অনুযায়ী ঘুরানো।

---

# 1. Rotation কী?

সহজ ভাষায়:

```text
Object
   ↓
ঘুরবে
   ↓
New Angle
```

যেমন একটি square:

```text
Before:

┌────┐
│    │
└────┘


After Rotation:

  ╲
   ╲
    ╲
```

Shape-এর **size একই থাকবে**, শুধু angle পরিবর্তন হবে।

---

# 2. OpenGL-এ Rotation

OpenGL-এ Rotation করার জন্য:

```cpp
glRotatef(angle, x, y, z);
```

ব্যবহার করি।

সবচেয়ে important হলো:

```cpp
glRotatef(45, 0.0, 0.0, 1.0);
```

এর মানে:

```text
45° → কত degree ঘুরবে

0.0 → X-axis

0.0 → Y-axis

1.0 → Z-axis
```

2D graphics-এর জন্য সাধারণত:

```text
Z = 1
```

রাখি।

---
