# Bresenham Circle Drawing Algorithm

> **Bresenham Circle Algorithm** হলো computer graphics-এ circle draw করার একটি efficient algorithm। এটি integer calculation এবং decision parameter ব্যবহার করে circle-এর points নির্বাচন করে।

আগের **Midpoint Circle**-এর মতো এখানেও সবচেয়ে important concept হলো:

```text
8-Way Symmetry
+
Decision Parameter
=
Circle
```

---

# 1. Bresenham Circle কী?

Bresenham Line Algorithm-এর মতোই Bresenham Circle Algorithm-ও pixel/point নির্বাচন করে circle আঁকে।

এখানে:

```text
sin() ❌
cos() ❌
Floating Point ❌
```

এর পরিবর্তে:

```text
Integer Calculation ✅
Decision Parameter ✅
8-Way Symmetry ✅
```

ব্যবহার করা হয়।

---

# 2. Circle-এর Basic Idea

ধরি circle-এর center:

```text
(xc, yc)
```

এবং radius:

```text
r
```

আমরা circle-এর পুরো অংশ calculate করব না।

শুধু **1/8 অংশ** calculate করব।

তারপর symmetry ব্যবহার করে একই point-এর 8টি position plot করব।

```text
1/8 Circle
    ↓
8 Symmetric Points
    ↓
Full Circle
```

---

# 3. 8-Way Symmetry

ধরি আমরা একটা point পেলাম:

```text
(x, y)
```

তাহলে circle-এর অন্য points:

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

Center `(xc,yc)` থাকলে:

```text
(xc+x, yc+y)
(xc-x, yc+y)
(xc+x, yc-y)
(xc-x, yc-y)

(xc+y, yc+x)
(xc-y, yc+x)
(xc+y, yc-x)
(xc-y, yc-x)
```

এই 8টা point একসাথে plot করলেই circle তৈরি হয়।

---

# 4. Starting Point

Bresenham Circle Algorithm-এর basic implementation-এ শুরু করি:

```text
x = 0
y = r
```

যেমন:

```text
r = 5
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

অর্থাৎ circle-এর top point।

---

# 5. Decision Parameter

এই algorithm-এর initial decision parameter:

```text
p = 3 - 2r
```

যেমন:

```text
r = 5
```

তাহলে:

```text
p = 3 - 2(5)

p = 3 - 10

p = -7
```

---

# 6. Decision Parameter কেন?

প্রতিবার আমাদের decide করতে হবে next point কোনটা হবে।

বর্তমান point:

```text
(x,y)
```

থেকে পরের point হতে পারে:

```text
(x+1, y)
```

অথবা:

```text
(x+1, y-1)
```

তাই `p` দেখে সিদ্ধান্ত নিই।

সহজভাবে:

```text
p < 0
↓
y same থাকবে

p >= 0
↓
y কমবে
```

---

# 7. Main Logic

সবচেয়ে important অংশ:

```text
p < 0
↓
x = x + 1
y = y
↓
p = p + 4x + 6
```

আর:

```text
p >= 0
↓
x = x + 1
y = y - 1
↓
p = p + 4(x-y) + 10
```

**খেয়াল রাখবে:** এই formula-গুলো code-এর `x++` / `y--` update-এর আগে/পরে কোন value ব্যবহার হচ্ছে তার উপর depend করে। নিচের code-এ আমরা আগে decision নিয়ে তারপর update করব, তাই formula এইভাবেই থাকবে।

---

# 8. Basic Code

```cpp
void DrawCircle(int xc, int yc, int r)
{
    int x = 0;                  // Starting X
    int y = r;                  // Starting Y = radius

    int p = 3 - 2 * r;          // Initial decision parameter

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

        // Decision parameter check
        if(p < 0)
        {
            // Y same থাকবে
            p = p + 4 * x + 6;

            // X এক ধাপ বাড়বে
            x++;
        }
        else
        {
            // Y এক ধাপ কমবে
            p = p + 4 * (x - y) + 10;

            x++;                // X এক ধাপ বাড়বে
            y--;                // Y এক ধাপ কমবে
        }
    }

    glEnd();                    // Point drawing শেষ
}
```

---

# 9. Function

```cpp
void DrawCircle(int xc, int yc, int r)
```

তিনটা parameter:

```text
xc → Center X
yc → Center Y
r  → Radius
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

# 10. `x = 0`

```cpp
int x = 0;
```

আমরা circle-এর top point থেকে শুরু করছি।

---

# 11. `y = r`

```cpp
int y = r;
```

যদি:

```text
r = 100
```

তাহলে:

```text
y = 100
```

Starting point:

```text
(0,100)
```

---

# 12. Initial Decision Parameter

```cpp
int p = 3 - 2 * r;
```

Formula:

```text
p = 3 - 2r
```

যদি:

```text
r = 5
```

তাহলে:

```text
p = 3 - 10
  = -7
```

---

# 13. `glBegin(GL_POINTS)`

```cpp
glBegin(GL_POINTS);
```

আমরা একেকটা point plot করে circle বানাচ্ছি।

তাই:

```text
GL_POINTS
```

ব্যবহার করছি।

---

# 14. `while(x <= y)`

```cpp
while(x <= y)
```

আমরা শুধু circle-এর 1/8 অংশ calculate করছি।

যখন:

```text
x > y
```

হবে, তখন ওই অংশের calculation শেষ।

তাই:

```text
x <= y
```

পর্যন্ত loop চলবে।

---

# 15. 8 Symmetric Points

```cpp
glVertex2i(xc + x, yc + y);
glVertex2i(xc - x, yc + y);
glVertex2i(xc + x, yc - y);
glVertex2i(xc - x, yc - y);

glVertex2i(xc + y, yc + x);
glVertex2i(xc - y, yc + x);
glVertex2i(xc + y, yc - x);
glVertex2i(xc - y, yc - x);
```

এগুলোকে শুধু এভাবে মনে রাখো:

```text
(x,y)
(-x,y)
(x,-y)
(-x,-y)

(y,x)
(-y,x)
(y,-x)
(-y,-x)
```

---

# 16. `if(p < 0)`

```cpp
if(p < 0)
```

এখন decision নেওয়া হচ্ছে।

যদি:

```text
p < 0
```

তাহলে:

```text
y same থাকবে
```

অর্থাৎ next point হবে:

```text
(x+1, y)
```

---

# 17. `p < 0` হলে Formula

```cpp
p = p + 4 * x + 6;
```

অর্থাৎ:

```text
p = p + 4x + 6
```

তারপর:

```cpp
x++;
```

মানে:

```text
x = x + 1
```

Y একই থাকবে।

---

# 18. `else`

```cpp
else
```

মানে:

```text
p >= 0
```

এবার:

```text
y--
```

অর্থাৎ Y এক কমবে।

Next point:

```text
(x+1, y-1)
```

---

# 19. `p >= 0` Formula

```cpp
p = p + 4 * (x - y) + 10;
```

অর্থাৎ:

```text
p = p + 4(x-y) + 10
```

তারপর:

```cpp
x++;
y--;
```

---

# 20. Main Logic

পুরো algorithm-টা:

```text
Start
 ↓
x = 0
y = r
 ↓
p = 3 - 2r
 ↓
8 points draw
 ↓
Check p
 ↓
┌──────────────────┐
│                  │
p < 0             p >= 0
│                  │
↓                  ↓
y same             y--
│                  │
↓                  ↓
p=p+4x+6       p=p+4(x-y)+10
│                  │
↓                  ↓
x++                x++
                    ↓
                   y--
        ↓
     Repeat
```

---

# 21. Example

ধরি:

```text
Center = (0,0)
Radius = 5
```

তাহলে:

```text
x = 0
y = 5
```

Initial:

```text
p = 3 - 2r
  = 3 - 10
  = -7
```

---

# 22. First Step

Current:

```text
x = 0
y = 5
p = -7
```

প্রথমে 8 symmetric points draw হবে।

তারপর:

```text
p < 0
```

তাই Y same থাকবে।

Formula:

```text
p = p + 4x + 6

p = -7 + 4(0) + 6

p = -1
```

তারপর:

```text
x = 1
y = 5
```

---

# 23. Second Step

Current:

```text
x = 1
y = 5
p = -1
```

আবার 8 points draw হবে।

`p < 0`, তাই:

```text
p = p + 4x + 6

p = -1 + 4(1) + 6

p = 9
```

তারপর:

```text
x = 2
y = 5
```

---

# 24. Third Step

এখন:

```text
x = 2
y = 5
p = 9
```

এবার:

```text
p >= 0
```

তাই Y কমবে।

Formula:

```text
p = p + 4(x-y) + 10

p = 9 + 4(2-5) + 10

p = 9 - 12 + 10

p = 7
```

তারপর:

```text
x = 3
y = 4
```

---

# 25. Example Table

Radius `5` এর জন্য:

| Step |  x |  y |  p | Decision |
| ---: | -: | -: | -: | -------- |
|    0 |  0 |  5 | -7 | `p < 0`  |
|    1 |  1 |  5 | -1 | `p < 0`  |
|    2 |  2 |  5 |  9 | `p >= 0` |
|    3 |  3 |  4 |  7 | `p >= 0` |
|    4 |  4 |  3 |  — | Stop     |

যখন:

```text
x > y
```

হয়ে যাবে, তখন loop stop করবে।

---

# 26. Visual Concept

Circle-এর 1/8 অংশ calculate করি:

```text
          ● ● ●
        ●
       ●
      ●
     ●
```

তারপর symmetry দিয়ে:

```text
          ● ● ●
       ●         ●
     ●             ●
    ●       +       ●
     ●             ●
       ●         ●
          ● ● ●
```

পুরো circle পাওয়া যায়।

---

# 27. Complete FreeGLUT Program

```cpp
#include <GL/glut.h>

// Bresenham Circle Drawing Algorithm
void DrawCircle(int xc, int yc, int r)
{
    int x = 0;                  // Starting X
    int y = r;                  // Starting Y

    int p = 3 - 2 * r;          // Initial decision parameter

    glBegin(GL_POINTS);         // Point drawing শুরু

    while(x <= y)
    {
        // 8 symmetric points
        glVertex2i(xc + x, yc + y);
        glVertex2i(xc - x, yc + y);
        glVertex2i(xc + x, yc - y);
        glVertex2i(xc - x, yc - y);

        glVertex2i(xc + y, yc + x);
        glVertex2i(xc - y, yc + x);
        glVertex2i(xc + y, yc - x);
        glVertex2i(xc - y, yc - x);

        // Decision parameter check
        if(p < 0)
        {
            // Y same থাকবে
            p = p + 4 * x + 6;

            // X বাড়বে
            x++;
        }
        else
        {
            // Decision parameter update
            p = p + 4 * (x - y) + 10;

            // X বাড়বে
            x++;

            // Y কমবে
            y--;
        }
    }

    glEnd();                    // Point drawing শেষ
}

void display()
{
    // Screen clear
    glClear(GL_COLOR_BUFFER_BIT);

    // Circle color
    glColor3f(1.0, 0.0, 0.0);

    // Point size
    glPointSize(2.0);

    // Circle draw
    DrawCircle(0, 0, 150);

    // Display
    glFlush();
}

void init()
{
    // Projection mode
    glMatrixMode(GL_PROJECTION);

    // Reset matrix
    glLoadIdentity();

    // Coordinate system
    gluOrtho2D(-400, 400, -300, 300);

    // Background color
    glClearColor(1.0, 1.0, 1.0, 1.0);
}

int main(int argc, char** argv)
{
    // GLUT initialize
    glutInit(&argc, argv);

    // Window size
    glutInitWindowSize(800, 600);

    // Window create
    glutCreateWindow("Bresenham Circle");

    // Initialization
    init();

    // Display function
    glutDisplayFunc(display);

    // Main loop
    glutMainLoop();

    return 0;
}
```

---

# 28. শুধু Algorithm অংশ মুখস্থ করার জন্য

```cpp
int x = 0;
int y = r;

int p = 3 - 2 * r;

while(x <= y)
{
    // 8 symmetric points

    if(p < 0)
    {
        p = p + 4 * x + 6;
        x++;
    }
    else
    {
        p = p + 4 * (x - y) + 10;
        x++;
        y--;
    }
}
```

এটাই Bresenham Circle-এর core।

---

# 29. Important Formula

### Starting Point

```text
x = 0
y = r
```

### Initial Decision Parameter

```text
p = 3 - 2r
```

### যদি `p < 0`

```text
y same

p = p + 4x + 6
x++
```

### যদি `p >= 0`

```text
x++
y--

p = p + 4(x-y) + 10
```

---

# 30. Midpoint Circle vs Bresenham Circle

এখানে exam-এর জন্য সবচেয়ে important comparison:

| বিষয়         | Midpoint Circle   | Bresenham Circle |
| ------------ | ----------------- | ---------------- |
| Starting `x` | `0`               | `0`              |
| Starting `y` | `r`               | `r`              |
| Initial `p`  | `1-r`             | `3-2r`           |
| Main concept | Midpoint decision | Integer decision |
| Symmetry     | 8-way             | 8-way            |
| `p < 0`      | Y same            | Y same           |
| `p >= 0`     | Y decreases       | Y decreases      |
| `sin/cos`    | No                | No               |
| `GL_POINTS`  | Yes               | Yes              |

সবচেয়ে important difference:

```text
Midpoint Circle
p = 1 - r
```

vs

```text
Bresenham Circle
p = 3 - 2r
```

---

# 31. Midpoint Circle-এর সাথে মিল

দুইটার common বিষয়:

```text
8-Way Symmetry
      +
Decision Parameter
      +
GL_POINTS
      +
Integer-based Calculation
```

---

# 32. কেন `sin()` / `cos()` ব্যবহার করি না?

কারণ algorithm-এর উদ্দেশ্য হলো:

```text
Integer calculation
+
Efficient point selection
```

তাই:

```cpp
cos()
sin()
```

এর পরিবর্তে decision parameter দিয়ে next point select করি।

---

# 33. Viva Questions

### Q1. Bresenham Circle Algorithm কী?

**Answer:**

> It is an efficient circle drawing algorithm that uses integer calculations and a decision parameter.

---

### Q2. Initial decision parameter কী?

**Answer:**

```text
p = 3 - 2r
```

---

### Q3. Starting point কী?

**Answer:**

```text
(x,y) = (0,r)
```

---

### Q4. Circle-এ কত-way symmetry ব্যবহার করি?

**Answer:**

> 8-way symmetry.

---

### Q5. `p < 0` হলে কী হয়?

**Answer:**

> X বাড়ে, Y same থাকে।

```text
x++
```

এবং:

```text
p = p + 4x + 6
```

---

### Q6. `p >= 0` হলে কী হয়?

**Answer:**

> X বাড়ে এবং Y কমে।

```text
x++
y--
```

এবং:

```text
p = p + 4(x-y) + 10
```

---

### Q7. Circle draw করতে কোন primitive ব্যবহার করেছি?

**Answer:**

```text
GL_POINTS
```

---

### Q8. Bresenham Circle-এ `sin()` এবং `cos()` ব্যবহার হয়?

**Answer:**

> No.

---

### Q9. কেন 8-way symmetry ব্যবহার করি?

**Answer:**

> একটি অংশের point calculate করে বাকি 7টি symmetric point পাওয়া যায়, তাই calculation কম লাগে।

---

### Q10. Midpoint Circle এবং Bresenham Circle-এর main difference কী?

**Answer:**

Initial decision parameter আলাদা:

```text
Midpoint:
p = 1-r

Bresenham:
p = 3-2r
```

---

# 34. Mid Exam Quick Revision

```text
           Bresenham Circle
                  ↓
             x = 0, y = r
                  ↓
              p = 3-2r
                  ↓
            8 Points Draw
                  ↓
              Check p
             /        \
          p < 0       p >= 0
            ↓             ↓
          y same         y--
            ↓             ↓
       p=p+4x+6    p=p+4(x-y)+10
            ↓             ↓
           x++           x++
                           ↓
                          y--
             ↓
           Repeat
```

---

# 35. One-Line Memory Trick

> **Bresenham Circle = ****x=0, y=r → p=3-2r → 8 points → p check → x++ / প্রয়োজনে y--**

আর Midpoint-এর সাথে শুধু initial formula মনে রাখো:

```text
Midpoint Circle
→ p = 1-r

Bresenham Circle
→ p = 3-2r
```

এই difference-টা **lab mid exam-এর আগে অবশ্যই clear রাখবে।**
