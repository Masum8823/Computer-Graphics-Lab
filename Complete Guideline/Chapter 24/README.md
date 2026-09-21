# Bresenham Line Drawing Algorithm

> **Bresenham Line Algorithm** হলো computer graphics-এ দুটি point-এর মধ্যে line draw করার একটি efficient algorithm।

DDA-এর সাথে এর সবচেয়ে important difference:

```text
DDA        → Floating Point calculation
Bresenham  → Integer calculation
```

তাই Bresenham সাধারণত DDA-এর চেয়ে **faster এবং efficient**।

---

# 1. Bresenham কী করে?

ধরি আমাদের দুটি point:

```text
Start Point → (x1, y1)

End Point   → (x2, y2)
```

Bresenham এই দুই point-এর মধ্যে কোন কোন pixel/point plot করতে হবে সেটা calculate করে।

সহজভাবে:

```text
Start
  ↓
Next pixel choose
  ↓
Next pixel choose
  ↓
Next pixel choose
  ↓
End
```

---
# 2. DDA-এর সাথে Main Difference

### DDA:

```text
dx
dy
steps
xIncrement
yIncrement
```

এবং decimal value ব্যবহার করে।

### Bresenham:

```text
dx
dy
Decision Parameter
```

এবং মূলত **integer calculation** ব্যবহার করে।

মনে রাখবে:

> **DDA → Floating Point**
> **Bresenham → Integer**

---


# 3. Bresenham-এর Basic Idea

ধরি line-এর slope:

```text
0 < m < 1
```

অর্থাৎ line খুব বেশি steep না।

তাহলে X direction-এ আমরা প্রতিবার:

```text
x = x + 1
```

করব।

কিন্তু Y কখন বাড়বে?

এই দুইটা option থাকবে:

```text
(x+1, y)
```

অথবা:

```text
(x+1, y+1)
```

Bresenham একটি **decision parameter `p`** ব্যবহার করে decide করে কোন point নিতে হবে।

---


# 4. Example

ধরি:

```text
Start = (2,2)

End = (8,5)
```

তাহলে:

```text
dx = 8 - 2 = 6

dy = 5 - 2 = 3
```

এখন প্রতিটি X step-এ Y হয়:

```text
same y
```

অথবা:

```text
y + 1
```

Bresenham `p` দেখে সিদ্ধান্ত নেয়।

---

# 5. Formula

যদি:

```text
dx > dy
```

তাহলে:

```text
p = 2dy - dx
```

এটাই initial decision parameter।

---
# 6. যদি `p < 0`

যদি:

```text
p < 0
```

তাহলে আমরা:

```text
(x+1, y)
```

point নেব।

অর্থাৎ:

```text
x বাড়বে
y একই থাকবে
```

তারপর:

```text
p = p + 2dy
```

---

# 7. যদি `p >= 0`

যদি:

```text
p >= 0
```

তাহলে:

```text
(x+1, y+1)
```

point নেব।

অর্থাৎ:

```text
x বাড়বে
y-ও বাড়বে
```

তারপর:

```text
p = p + 2dy - 2dx
```

---
# 8. Main Logic

এটা খুব ভালো করে বুঝবে:

```text
p < 0
 ↓
(x+1, y)
 ↓
p = p + 2dy


p >= 0
 ↓
(x+1, y+1)
 ↓
p = p + 2dy - 2dx
```

এটাই Bresenham-এর main logic।

---
# 9. Basic Code

এখন basic Bresenham code:

```cpp
void DrawLine(int x1, int y1, int x2, int y2)
{
    int dx = x2 - x1;              // X direction-এর distance
    int dy = y2 - y1;              // Y direction-এর distance

    int p = 2 * dy - dx;            // Initial decision parameter

    int x = x1;                    // Starting X
    int y = y1;                    // Starting Y

    glBegin(GL_POINTS);            // Point drawing শুরু

    while(x <= x2)
    {
        glVertex2i(x, y);          // Current point draw

        x++;                       // X সবসময় 1 করে বাড়বে

        if(p < 0)
        {
            // p negative হলে Y change হবে না
            p = p + 2 * dy;
        }
        else
        {
            // p positive হলে Y 1 করে বাড়বে
            y++;
            p = p + 2 * dy - 2 * dx;
        }
    }

    glEnd();                       // Point drawing শেষ
}
```

---

# 10. এখন Line by Line

## Header

```cpp
#include <GL/glut.h>
```

OpenGL/FreeGLUT-এর functions ব্যবহার করার জন্য।

---

# 11. Function

```cpp
void DrawLine(int x1, int y1, int x2, int y2)
```

চারটি coordinate নিচ্ছে:

```text
(x1,y1) → Starting Point

(x2,y2) → Ending Point
```

---

# 12. `dx`

```cpp
int dx = x2 - x1;
```

X-axis বরাবর distance।

Example:

```text
x1 = 2
x2 = 8

dx = 8 - 2
   = 6
```

---

# 13. `dy`

```cpp
int dy = y2 - y1;
```

Y-axis বরাবর distance।

Example:

```text
y1 = 2
y2 = 5

dy = 5 - 2
   = 3
```

---

# 14. Initial `p`

```cpp
int p = 2 * dy - dx;
```

এটা Bresenham-এর **decision parameter**।

Formula:

```text
p = 2dy - dx
```

Example:

```text
dx = 6
dy = 3

p = 2(3) - 6
  = 6 - 6
  = 0
```

---
# 15. Starting X

```cpp
int x = x1;
```

মানে:

```text
x = starting X
```

---

# 16. Starting Y

```cpp
int y = y1;
```

মানে:

```text
y = starting Y
```

অর্থাৎ শুরু করছি:

```text
(x,y) = (x1,y1)
```

---
# 17. `glBegin(GL_POINTS)`

```cpp
glBegin(GL_POINTS);
```

Bresenham algorithm আমরা একেকটা pixel/point plot করে line বানাচ্ছি।

তাই:

```text
GL_POINTS
```

ব্যবহার করছি।

---
# 18. `while`

```cpp
while(x <= x2)
```

যতক্ষণ X শেষ point পর্যন্ত যায়, loop চলবে।

---

# 19. Current Point Draw

```cpp
glVertex2i(x, y);
```

Current `(x,y)` point draw করবে।

এখানে:

```text
2i → 2D Integer coordinate
```

কারণ Bresenham integer coordinate ব্যবহার করে।

---

# 20. X Increase

```cpp
x++;
```

এর মানে:

```text
x = x + 1
```

Bresenham-এর এই case-এ প্রতিবার X এক করে বাড়ছে।

---
# 21. `if(p < 0)`

```cpp
if(p < 0)
```

এখন algorithm decision নিচ্ছে।

যদি:

```text
p < 0
```

তাহলে:

```text
(x+1, y)
```

নেব।

অর্থাৎ:

```text
X → বাড়বে
Y → একই থাকবে
```

---

# 22. `p` Update যখন Negative

```cpp
p = p + 2 * dy;
```

অর্থাৎ:

```text
p = p + 2dy
```

---
# 23. `else`

```cpp
else
```

মানে:

```text
p >= 0
```

তখন:

```text
(x+1, y+1)
```

নেব।

অর্থাৎ:

```text
X → +1
Y → +1
```

---

# 24. Y Increase

```cpp
y++;
```

মানে:

```text
y = y + 1
```

---

# 25. `p` Update যখন Positive

```cpp
p = p + 2 * dy - 2 * dx;
```

Formula:

```text
p = p + 2dy - 2dx
```

---

# 26. Full Logic এক নজরে

```text
Current Point
     ↓
Check p
     ↓
┌───────────────┐
│               │
p < 0          p >= 0
│               │
↓               ↓
(x+1,y)      (x+1,y+1)
│               │
↓               ↓
p=p+2dy     p=p+2dy-2dx
```

---