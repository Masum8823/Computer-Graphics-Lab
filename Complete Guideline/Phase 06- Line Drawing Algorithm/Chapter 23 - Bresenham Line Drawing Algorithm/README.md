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

# 27. Example হাতে করি

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

Initial:

```text
p = 2dy - dx

p = 2(3) - 6

p = 0
```

Starting:

```text
x = 2
y = 2
```

---

# 28. প্রথম Point

Plot:

```text
(2,2)
```

এখন:

```text
p = 0
```

যেহেতু:

```text
p >= 0
```

তাই:

```text
x = 3
y = 3
```

এবং:

```text
p = p + 2dy - 2dx

p = 0 + 6 - 12

p = -6
```

Next:

```text
(3,3)
```

---

# 29. দ্বিতীয় Decision

এখন:

```text
p = -6
```

তাই:

```text
p < 0
```

সুতরাং:

```text
x = 4
y = 3
```

Y change হলো না।

p:

```text
p = p + 2dy

p = -6 + 6

p = 0
```

Next:

```text
(4,3)
```

---

# 30. Table

এই example-এর pointগুলো:

| Step | Point |  p | Decision |
| ---: | ----- | -: | -------- |
|    0 | (2,2) |  0 | Y বাড়ে   |
|    1 | (3,3) | -6 | Y same   |
|    2 | (4,3) |  0 | Y বাড়ে   |
|    3 | (5,4) | -6 | Y same   |
|    4 | (6,4) |  0 | Y বাড়ে   |
|    5 | (7,5) | -6 | Y same   |
|    6 | (8,5) |  0 | End      |

তাই line-এর points:

```text
(2,2)
(3,3)
(4,3)
(5,4)
(6,4)
(7,5)
(8,5)
```

---
# 31. Visual

```text
Y
↑
5 |                    ● ●
4 |              ● ●
3 |        ● ●
2 |    ●
1 |
  +--------------------------→ X
     2  3  4  5  6  7  8
```

এই points-গুলো খুব কাছাকাছি থাকায় চোখে line-এর মতো দেখা যায়।

---
# 32. কেন `p` দরকার?

এটাই সবচেয়ে important concept।

প্রতিবার আমাদের সামনে দুইটা possible point:

```text
(x+1, y)
```

অথবা:

```text
(x+1, y+1)
```

Bresenham `p` দেখে decide করে কোনটা line-এর কাছাকাছি।

তাই:

> **`p` = Decision Parameter**

---

# 33. `p < 0` হলে কী হয়?

```text
p < 0
```

তাহলে:

```text
(x+1, y)
```

নেব।

মানে:

```text
x → +1

y → same
```

Code:

```cpp
p = p + 2 * dy;
```

---

# 34. `p >= 0` হলে কী হয়?

```text
p >= 0
```

তাহলে:

```text
(x+1, y+1)
```

নেব।

মানে:

```text
x → +1

y → +1
```

Code:

```cpp
y++;

p = p + 2 * dy - 2 * dx;
```

---

# 35. কেন `while(x <= x2)`?

এই basic version-এ আমরা ধরে নিচ্ছি:

```text
x2 > x1
```

এবং:

```text
0 < slope < 1
```

অর্থাৎ:

```text
dx > dy
```

তাই X direction-এ এগোতে থাকি:

```text
x1 → x1+1 → x1+2 → ... → x2
```

---

# 36. Important Condition

এই basic Bresenham code-এর জন্য সাধারণত:

```text
0 < m < 1
```

অর্থাৎ:

```text
0 < dy/dx < 1
```

এবং:

```text
dx > dy
```

ধরা হয়।

---

# 37. Negative Slope হলে?

যদি:

```text
dy < 0
```

তাহলে Y কমবে।

তখন:

```cpp
y--;
```

ব্যবহার করতে হবে।

কিন্তু **lab exam-এর basic implementation**-এ অনেক সময় প্রথমে `0 < m < 1` case-টাই শেখানো হয়।

---

# 38. Vertical Line?

যদি:

```text
x1 = x2
```

তাহলে:

```text
dx = 0
```

এই basic code দিয়ে সেটা handle করা যাবে না।

কারণ এই version:

```text
dx > dy
```

case ধরে লেখা।

---
# 39. General Bresenham Algorithm

যদি সব ধরনের line handle করতে চাই, তাহলে একটু advanced code লাগবে।

সেখানে handle করতে হবে:

```text
Positive slope
Negative slope
Steep slope
Shallow slope
Horizontal line
Vertical line
```

কিন্তু তোমার **basic lab exam-এর জন্য** আগে এই version ভালোভাবে বুঝে রাখো।

---

# 40. Complete FreeGLUT Program

```cpp
#include <GL/glut.h>

// Bresenham Line Drawing
void DrawLine(int x1, int y1, int x2, int y2)
{
    // X distance
    int dx = x2 - x1;

    // Y distance
    int dy = y2 - y1;

    // Initial decision parameter
    int p = 2 * dy - dx;

    // Starting point
    int x = x1;
    int y = y1;

    // Point drawing শুরু
    glBegin(GL_POINTS);

    // X শেষ point পর্যন্ত যাবে
    while(x <= x2)
    {
        // Current point draw
        glVertex2i(x, y);

        // X সবসময় 1 করে বাড়বে
        x++;

        // Decision
        if(p < 0)
        {
            // Y একই থাকবে
            p = p + 2 * dy;
        }
        else
        {
            // Y 1 করে বাড়বে
            y++;

            // Decision parameter update
            p = p + 2 * dy - 2 * dx;
        }
    }

    // Point drawing শেষ
    glEnd();
}

void display()
{
    // Screen clear
    glClear(GL_COLOR_BUFFER_BIT);

    // Line color
    glColor3f(1.0, 0.0, 0.0);

    // Point size
    glPointSize(3.0);

    // Bresenham line
    DrawLine(-200, -100, 200, 150);

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
    glutCreateWindow("Bresenham Line");

    // Initialize
    init();

    // Display function
    glutDisplayFunc(display);

    // Main loop
    glutMainLoop();

    return 0;
}
```

---

# 41. DDA vs Bresenham

এটা exam-এ খুব important।

| বিষয়          | DDA                           | Bresenham                |
| ------------- | ----------------------------- | ------------------------ |
| Full Form     | Digital Differential Analyzer | Bresenham Line Algorithm |
| Calculation   | Floating Point                | Integer                  |
| Main idea     | Increment                     | Decision Parameter       |
| Main variable | xIncrement, yIncrement        | `p`                      |
| Speed         | তুলনামূলক slow                | তুলনামূলক fast           |
| Accuracy      | ভালো                          | ভালো                     |
| Point drawing | `GL_POINTS`                   | `GL_POINTS`              |

সবচেয়ে important:

```text
DDA
↓
Floating Point
↓
Increment


Bresenham
↓
Integer
↓
Decision Parameter
```

---
# 42. DDA-এর Code বনাম Bresenham Code

### DDA

```cpp
float xIncrement = dx / (float)steps;
float yIncrement = dy / (float)steps;

x = x + xIncrement;
y = y + yIncrement;
```

### Bresenham

```cpp
int p = 2 * dy - dx;

if(p < 0)
{
    p = p + 2 * dy;
}
else
{
    y++;
    p = p + 2 * dy - 2 * dx;
}
```

তাই সহজে মনে রাখবে:

> **DDA → Increment দিয়ে line**
> **Bresenham → Decision Parameter দিয়ে line**

---

# 43. Bresenham Algorithm Steps

```text
Step 1:
dx = x2 - x1
dy = y2 - y1

Step 2:
p = 2dy - dx

Step 3:
x = x1
y = y1

Step 4:
Plot(x,y)

Step 5:
x = x + 1

Step 6:
If p < 0:
    p = p + 2dy

Otherwise:
    y = y + 1
    p = p + 2dy - 2dx

Step 7:
Repeat until x = x2
```

---

# 44. সবচেয়ে Important Formula

### `dx`

```text
dx = x2 - x1
```

### `dy`

```text
dy = y2 - y1
```

### Initial Decision Parameter

```text
p = 2dy - dx
```

### যদি `p < 0`

```text
p = p + 2dy
```

### যদি `p >= 0`

```text
p = p + 2dy - 2dx
```

এগুলো **অবশ্যই মুখস্থ** রাখবে।

---

# 45. Viva Questions

### Q1. Bresenham কী?

**Answer:**

> Bresenham is a line drawing algorithm used to draw a line between two points using mainly integer calculations.

---

### Q2. Bresenham-এর main advantage কী?

**Answer:**

> It uses integer arithmetic, so it is faster and more efficient than DDA.

---

### Q3. Bresenham-এর decision parameter কী?

**Answer:**

```text
p = 2dy - dx
```

---

### Q4. `p < 0` হলে কী করি?

**Answer:**

```text
(x+1, y)
```

নিই এবং:

```text
p = p + 2dy
```

---

### Q5. `p >= 0` হলে কী করি?

**Answer:**

```text
(x+1, y+1)
```

নিই এবং:

```text
p = p + 2dy - 2dx
```

---

### Q6. Bresenham-এ floating point লাগে?

**Answer:**

> No. Basic Bresenham uses integer calculations.

---

### Q7. `p` কী?

**Answer:**

> `p` is the decision parameter used to select the next pixel.

---

### Q8. Bresenham-এ কোন OpenGL primitive ব্যবহার করা হয়েছে?

**Answer:**

```text
GL_POINTS
```

---

### Q9. `glVertex2i()` কেন ব্যবহার করেছি?

**Answer:**

> Bresenham integer coordinates নিয়ে কাজ করে, তাই `glVertex2i()` ব্যবহার করা হয়েছে।

---

### Q10. DDA এবং Bresenham-এর main difference?

**Answer:**

```text
DDA → Floating Point

Bresenham → Integer
```

---

# 46. Mid Exam Quick Revision

শুধু এগুলো দেখলেই Bresenham-এর পুরো concept মনে পড়ে যাবে:

```text
Bresenham
    ↓
Two Points
    ↓
dx = x2 - x1
dy = y2 - y1
    ↓
p = 2dy - dx
    ↓
p < 0 ?
 ┌──────────────┐
 Yes            No
 ↓               ↓
(x+1,y)       (x+1,y+1)
 ↓               ↓
p=p+2dy       y++
               ↓
          p=p+2dy-2dx
```

---
# 47. এক লাইনে মনে রাখো

> **Bresenham = `dx, dy → p → p check → next pixel select → line draw`**

আর DDA-এর সাথে:

```text
DDA        → Increment
Bresenham  → Decision Parameter
```

এই দুইটা difference মাথায় থাকলে lab viva-তে অনেক সহজে answer দিতে পারবে।