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
# 19. তৃতীয় Point

```cpp
glVertex2i(xc + x, yc - y);
```

এখানে:

```text
(+x,-y)
```

---
# 20. চতুর্থ Point

```cpp
glVertex2i(xc - x, yc - y);
```

এখানে:

```text
(-x,-y)
```

---

# 21. বাকি 4 Point

এখন X এবং Y swap করি।

```cpp
glVertex2i(xc + y, yc + x);
glVertex2i(xc - y, yc + x);
glVertex2i(xc + y, yc - x);
glVertex2i(xc - y, yc - x);
```

এগুলো:

```text
(+y,+x)
(-y,+x)
(+y,-x)
(-y,-x)
```

---

# 22. সব 8 Point একসাথে

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

# 23. `x++`

```cpp
x++;
```

মানে:

```text
x = x + 1
```

প্রতিবার আমরা X direction-এ এক ধাপ এগোচ্ছি।

---
# 24. `if(p < 0)`

```cpp
if(p < 0)
```

Decision parameter check করছি।

যদি:

```text
p < 0
```

তাহলে next point হবে **East direction**-এর।

সহজভাবে:

```text
x → +1
y → same
```

---

# 25. `p < 0` হলে

```cpp
p = p + 2 * x + 1;
```

অর্থাৎ:

```text
p = p + 2x + 1
```

---

# 26. `else`

```cpp
else
```

মানে:

```text
p >= 0
```

এবার South-East point নিতে হবে।

অর্থাৎ:

```text
x → +1
y → -1
```

---

# 27. `y--`

```cpp
y--;
```

মানে:

```text
y = y - 1
```

---

# 28. Decision Parameter Update

```cpp
p = p + 2 * x + 1 - 2 * y;
```

অর্থাৎ:

```text
p = p + 2x + 1 - 2y
```

---

# 29. Complete Logic

```text
Start
 ↓
x = 0
y = r
p = 1-r
 ↓
8 points plot
 ↓
x++
 ↓
p check
 ↓
┌─────────────────┐
│                 │
p < 0            p >= 0
│                 │
↓                 ↓
y same           y--
│                 │
↓                 ↓
p=p+2x+1      p=p+2x+1-2y
│                 │
└────────┬────────┘
         ↓
     Repeat
```

---

# 30. Example

ধরি:

```text
Center = (0,0)
Radius = 5
```

তাহলে:

```text
x = 0
y = 5
p = 1 - 5
  = -4
```

Starting point:

```text
(0,5)
```

---

# 31. First Iteration

Current:

```text
x = 0
y = 5
p = -4
```

প্রথমে 8 symmetric point plot হবে।

তারপর:

```text
x++
```

তাই:

```text
x = 1
```

এখন:

```text
p < 0
```

তাই Y same থাকবে:

```text
y = 5
```

Update:

```text
p = p + 2x + 1

p = -4 + 2(1) + 1

p = -1
```

---

# 32. Second Iteration

এখন:

```text
x = 1
y = 5
p = -1
```

আবার 8 points plot হবে।

তারপর:

```text
x++
```

তাই:

```text
x = 2
```

এখন:

```text
p < 0
```

তাই:

```text
y = 5
```

Update:

```text
p = -1 + 2(2) + 1

p = 4
```

---

# 33. Third Iteration

এখন:

```text
x = 2
y = 5
p = 4
```

`p >= 0`, তাই:

```text
y--
```

অর্থাৎ:

```text
y = 4
```

তারপর:

```text
p = p + 2x + 1 - 2y

p = 4 + 2(2) + 1 - 2(4)

p = 1
```

---

# 34. Example Table

Radius `5` হলে approximate calculation:

| Step |  x |  y |  p | Decision |
| ---: | -: | -: | -: | -------- |
|    0 |  0 |  5 | -4 | `p < 0`  |
|    1 |  1 |  5 | -1 | `p < 0`  |
|    2 |  2 |  5 |  4 | `p >= 0` |
|    3 |  3 |  4 |  3 | `p >= 0` |
|    4 |  4 |  3 |  — | Stop     |

Loop তখন stop করবে যখন:

```text
x > y
```

---

# 35. Circle দেখতে কেমন হবে?

Conceptually:

```text
             ● ● ●
          ●         ●
        ●             ●
       ●               ●
      ●        +        ●
       ●               ●
        ●             ●
          ●         ●
             ● ● ●
```

`+` হলো center।

---

# 36. Complete FreeGLUT Program

```cpp
#include <GL/glut.h>

// Midpoint Circle Algorithm
void DrawCircle(int xc, int yc, int r)
{
    int x = 0;                  // Starting X
    int y = r;                  // Starting Y

    int p = 1 - r;              // Initial decision parameter

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

        // X এক করে বাড়বে
        x++;

        // Decision parameter check
        if(p < 0)
        {
            // Y same থাকবে
            p = p + 2 * x + 1;
        }
        else
        {
            // Y এক করে কমবে
            y--;

            // Decision parameter update
            p = p + 2 * x + 1 - 2 * y;
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

    // Reset
    glLoadIdentity();

    // Coordinate system
    gluOrtho2D(-400, 400, -300, 300);

    // Background
    glClearColor(1.0, 1.0, 1.0, 1.0);
}

int main(int argc, char** argv)
{
    // GLUT initialize
    glutInit(&argc, argv);

    // Window size
    glutInitWindowSize(800, 600);

    // Window create
    glutCreateWindow("Midpoint Circle");

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

# 37. সবচেয়ে Important Code

Midpoint Circle-এর শুধু algorithm অংশ যদি মনে রাখতে চাও:

```cpp
int x = 0;
int y = r;

int p = 1 - r;

while(x <= y)
{
    // 8 symmetric points draw

    x++;

    if(p < 0)
    {
        p = p + 2*x + 1;
    }
    else
    {
        y--;
        p = p + 2*x + 1 - 2*y;
    }
}
```

---

# 38. Important Formula

Midterm-এর জন্য এগুলো **অবশ্যই মুখস্থ**:

### Starting Point

```text
x = 0
y = r
```

### Initial Decision Parameter

```text
p = 1 - r
```

### যদি `p < 0`

```text
x = x + 1
y = y

p = p + 2x + 1
```

### যদি `p >= 0`

```text
x = x + 1
y = y - 1

p = p + 2x + 1 - 2y
```

---

# 39. 8 Symmetric Points

এটাও খুব important:

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

Center থাকলে:

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

---

# 40. কেন 8 Point?

কারণ circle-এর:

```text
8-way symmetry
```

আছে।

একটি octant-এর একটি point জানলেই symmetry ব্যবহার করে একই সাথে 8টি point পাওয়া যায়।

তাই পুরো circle আলাদাভাবে calculate করতে হয় না।

---

# 41. Midpoint Circle বনাম Normal Circle

আগের circle code:

```cpp
float angle = i * 3.1416 / 180.0;

float x = xc + r * cos(angle);
float y = yc + r * sin(angle);
```

এখানে:

```text
sin()
cos()
angle
```

ব্যবহার হয়েছে।

Midpoint Circle:

```cpp
int p = 1 - r;
```

এবং:

```text
p < 0
p >= 0
```

দিয়ে next point select করে।

---

# 42. Midpoint Circle বনাম DDA

| DDA Line           | Midpoint Circle              |
| ------------------ | ---------------------------- |
| Line draw করে      | Circle draw করে              |
| `dx`, `dy` ব্যবহার | `r`, `p` ব্যবহার             |
| Increment ব্যবহার  | Decision parameter           |
| Floating point     | Integer-based                |
| Line-এর points     | Circle-এর 8 symmetric points |

---

# 43. Viva Questions

### Q1. Midpoint Circle Algorithm কী?

**Answer:**

> Midpoint Circle Algorithm is an efficient algorithm used to draw a circle using decision parameters and symmetry.

---

### Q2. Starting point কী?

**Answer:**

```text
(x,y) = (0,r)
```

---

### Q3. Initial decision parameter কী?

**Answer:**

```text
p = 1 - r
```

---

### Q4. Circle-এর কত-way symmetry ব্যবহার করি?

**Answer:**

> 8-way symmetry.

---

### Q5. কেন 8-way symmetry ব্যবহার করি?

**Answer:**

> একটি অংশ calculate করে symmetry ব্যবহার করে বাকি অংশের points পাওয়া যায়।

---

### Q6. `p < 0` হলে কী হয়?

**Answer:**

> X বাড়ে, Y same থাকে।

```text
x++
```

এবং:

```text
p = p + 2x + 1
```

---

### Q7. `p >= 0` হলে কী হয়?

**Answer:**

> X বাড়ে এবং Y কমে।

```text
x++
y--
```

এবং:

```text
p = p + 2x + 1 - 2y
```

---

### Q8. Circle draw করতে কোন primitive ব্যবহার করেছি?

**Answer:**

```text
GL_POINTS
```

---

### Q9. Midpoint Circle-এ `sin()` এবং `cos()` ব্যবহার করেছি?

**Answer:**

> No.

---

### Q10. Circle-এর center কীভাবে pass করি?

**Answer:**

```cpp
DrawCircle(xc, yc, r);
```

যেখানে:

```text
xc → center X
yc → center Y
r  → radius
```

---

# 44. Mid Exam Quick Revision

```text
        Midpoint Circle
               ↓
        x = 0, y = r
               ↓
          p = 1 - r
               ↓
       8 points plot
               ↓
             x++
               ↓
          Check p
          /       \
       p < 0     p >= 0
        ↓           ↓
      y same       y--
        ↓           ↓
    p=p+2x+1    p=p+2x+1-2y
        ↓           ↓
        └─────┬─────┘
              ↓
           Repeat
```

---

# 45. One-Line Memory Trick

> **Midpoint Circle = ****x=0, y=r → p=1-r → 8 points → p check → x++ / y--**

আর সবচেয়ে important:

```text
8-Way Symmetry
+
Decision Parameter
=
Midpoint Circle
```
