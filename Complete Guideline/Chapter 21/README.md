# Scaling

> Scaling হলো কোনো object/shape-এর **size বড় বা ছোট করা**।

---

# 1. Scaling কী?

সহজ ভাষায়:

```text
Object
   ↓
Size Change
   ↓
Scaling
```

যেমন:

```text
Before:

  ┌───┐
  │   │
  └───┘


After Scaling:

  ┌───────┐
  │       │
  │       │
  └───────┘
```

Object-এর shape একই থাকবে, কিন্তু **size change হবে**।

---

# 2. OpenGL-এ Scaling

OpenGL-এ Scaling করার function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
Sx → X direction-এ কত গুণ বড়/ছোট হবে

Sy → Y direction-এ কত গুণ বড়/ছোট হবে

Sz → Z direction-এ কত গুণ বড়/ছোট হবে
```

2D graphics-এর ক্ষেত্রে সাধারণত:

```cpp
glScalef(Sx, Sy, 1.0);
```

ব্যবহার করি।

---
# 2. OpenGL-এ Scaling

OpenGL-এ Scaling করার function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
Sx → X direction-এ কত গুণ বড়/ছোট হবে

Sy → Y direction-এ কত গুণ বড়/ছোট হবে

Sz → Z direction-এ কত গুণ বড়/ছোট হবে
```

2D graphics-এর ক্ষেত্রে সাধারণত:

```cpp
glScalef(Sx, Sy, 1.0);
```

ব্যবহার করি।

---
