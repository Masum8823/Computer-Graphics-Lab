# Midpoint Circle Drawing Algorithm

> **Midpoint Circle Algorithm** হলো computer graphics-এ একটি circle draw করার algorithm।

আমরা আগে সাধারণভাবে circle এভাবে এঁকেছিলাম:

```cpp
for(int i = 0; i < 360; i++)
{
    float angle = i * 3.1416 / 180.0;

    float x = xc + r * cos(angle);
    float y = yc + r * sin(angle);

    glVertex2f(x, y);
}
```

এখানে `sin()` এবং `cos()` ব্যবহার করেছি।

কিন্তু **Midpoint Circle Algorithm**-এ আমরা এইভাবে circle draw করি না।

এখানে মূল idea:

```text
Decision Parameter
        ↓
Next Point নির্বাচন
        ↓
Circle Draw
```

---

# 1. Circle-এর Basic Equation

Mathematics-এ circle-এর equation:

```text
(x - xc)² + (y - yc)² = r²
```

যেখানে:

```text
(xc, yc) → Circle Center

r → Radius
```

কিন্তু পুরো equation বারবার calculate না করে Midpoint Algorithm একটা **decision parameter ****`p`** ব্যবহার করে।

---
# 2. Main Idea

Circle-এর পুরো অংশ একসাথে calculate করার দরকার নেই।

একটা অংশ calculate করলেই symmetry-এর কারণে বাকি অংশগুলো পাওয়া যায়।

Circle-এর একটি point:

```text
(x, y)
```

থাকলে একই ধরনের আরও 7টি point পাওয়া যায়।

অর্থাৎ:

```text
8 Symmetric Points
```

এই কারণে Midpoint Circle Algorithm খুব efficient।

---
# 3. 8-Way Symmetry

ধরি আমরা একটি point পেলাম:

```text
(x, y)
```

তাহলে একই circle-এর আরও point:

```text
(x, y)
(-x, y)
(x, -y)
(-x, -y)

(y, x)
(-y, x)
(y, -x)
(-y, -x)
```

Center যদি `(xc, yc)` হয়, তাহলে center-এর সাথে যোগ হবে।

---