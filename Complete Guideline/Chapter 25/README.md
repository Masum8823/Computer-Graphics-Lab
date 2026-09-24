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

# 4. Example

ধরি:

```text
Center = (0,0)

Radius = 5
```

একটি point যদি হয়:

```text
(3,4)
```

তাহলে circle-এর symmetric points:

```text
(3,4)
(-3,4)
(3,-4)
(-3,-4)

(4,3)
(-4,3)
(4,-3)
(-4,-3)
```

এই 8টা point একই circle-এর উপর থাকবে।

---

# 5. কেন শুধু 1/8 Circle calculate করি?

Circle দেখতে:

```text
        ● ● ●
     ●       ●
   ●           ●
  ●      +      ●
   ●           ●
     ●       ●
        ● ● ●
```

Circle-এর একটা ছোট অংশ calculate করলেই symmetry দিয়ে পুরো circle পাওয়া যায়।

তাই:

```text
1/8 অংশ calculate
        ↓
8টি symmetric point plot
        ↓
Full Circle
```

---

# 6. Starting Point

Midpoint Circle Algorithm-এ আমরা শুরু করি:

```text
x = 0
y = r
```

অর্থাৎ circle-এর top point থেকে।

যদি:

```text
center = (0,0)
radius = 5
```

তাহলে:

```text
x = 0
y = 5
```

Starting point:

```text
(0,5)
```

---
# 7. Initial Decision Parameter

Basic Midpoint Circle Algorithm-এর জন্য:

```text
p = 1 - r
```

অর্থাৎ:

```cpp
p = 1 - r;
```

যদি:

```text
r = 5
```

তাহলে:

```text
p = 1 - 5
  = -4
```

---

# 8. Decision কী?

প্রতিবার আমাদের next point choose করতে হবে।

দুটি possible direction:

```text
E  → East
SE → South-East
```

সহজভাবে:

```text
p < 0
↓
East point

p >= 0
↓
South-East point
```

অর্থাৎ:

```text
p < 0
→ x বাড়বে
→ y একই থাকবে

p >= 0
→ x বাড়বে
→ y কমবে
```

---

# 9. Main Logic

এটা খুব ভালোভাবে মনে রাখবে:

```text
p < 0
↓
x = x + 1
y = y
↓
p = p + 2x + 1
```

আর:

```text
p >= 0
↓
x = x + 1
y = y - 1
↓
p = p + 2x + 1 - 2y
```

**Note:** এখানে update-এর আগে/পরে `x,y` কোন value ব্যবহার হচ্ছে সেটা code-এর order-এর উপর নির্ভর করে। নিচের code-এ আমরা আগে `x++/y--` করে তারপর formula update করব।

তাই code অনুযায়ী formula হবে:

```text
p = p + 2x + 1
```

অথবা:

```text
p = p + 2x + 1 - 2y
```

---
# 10. Basic Code

```cpp
void DrawCircle(int xc, int yc, int r)
{
    int x = 0;                  // Starting X
    int y = r;                  // Starting Y = radius

    int p = 1 - r;              // Initial decision parameter

    glBegin(GL_POINTS);         // Point drawing শুরু

    while(x <= y)
    {
        // 8টি symmetric point draw
        glVertex2i(xc + x, yc + y);
        glVertex2i(xc - x, yc + y);
        glVertex2i(xc + x, yc - y);
        glVertex2i(xc - x, yc - y);

        glVertex2i(xc + y, yc + x);
        glVertex2i(xc - y, yc + x);
        glVertex2i(xc + y, yc - x);
        glVertex2i(xc - y, yc - x);

        // X এক ধাপ বাড়বে
        x++;

        if(p < 0)
        {
            // East point নেওয়া হয়েছে
            p = p + 2 * x + 1;
        }
        else
        {
            // South-East point নেওয়া হয়েছে
            y--;

            p = p + 2 * x + 1 - 2 * y;
        }
    }

    glEnd();                    // Point drawing শেষ
}
```

---

# 11. Code Line by Line

## Function

```cpp
void DrawCircle(int xc, int yc, int r)
```

তিনটা parameter:

```text
xc → Center-এর X

yc → Center-এর Y

r → Radius
```

যেমন:

```cpp
DrawCircle(0, 0, 100);
```

মানে:

```text
Center = (0,0)
Radius = 100
```

---

# 12. `x = 0`

```cpp
int x = 0;
```

আমরা circle-এর top point থেকে শুরু করছি।

---

# 13. `y = r`

```cpp
int y = r;
```

Radius যদি:

```text
r = 100
```

হয়:

```text
y = 100
```

Starting point:

```text
(0,100)
```

Center `(0,0)` হলে এটা circle-এর top point।

---

# 14. `p = 1-r`

```cpp
int p = 1 - r;
```

এটা হলো initial decision parameter।

Formula:

```text
p = 1 - r
```

যেমন:

```text
r = 100

p = 1 - 100
  = -99
```

---

# 15. `glBegin(GL_POINTS)`

```cpp
glBegin(GL_POINTS);
```

আমরা point plot করে circle তৈরি করছি।

তাই:

```text
GL_POINTS
```

ব্যবহার করছি।

---

# 16. `while(x <= y)`

```cpp
while(x <= y)
```

আমরা শুধু circle-এর **1/8 অংশ** calculate করছি।

যখন:

```text
x > y
```

হয়ে যাবে, তখন ওই অংশ শেষ।

তাই loop condition:

```text
x <= y
```

---
# 17. প্রথম Symmetric Point

```cpp
glVertex2i(xc + x, yc + y);
```

এটা প্রথম point।

যদি:

```text
xc = 0
yc = 0
x = 0
y = 5
```

তাহলে:

```text
(0+0, 0+5)
= (0,5)
```

---

# 18. দ্বিতীয় Point

```cpp
glVertex2i(xc - x, yc + y);
```

এখানে X-এর negative side।

```text
(-x,+y)
```

---
