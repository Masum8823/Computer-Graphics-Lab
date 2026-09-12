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



# 3. সহজে মনে রাখো

Transformation তিনটা:

```text
Translation → Position Change
Rotation    → Angle Change
Scaling     → Size Change
```

অর্থাৎ:

```text
T → Move
R → Rotate
S → Size
```

---


# 4. Simple Scaling Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);

    // Current transformation save
    glPushMatrix();

    // Object-এর size 2 গুণ বড় করবে
    // X = 2, Y = 2
    glScalef(2.0, 2.0, 1.0);

    // Red Color
    glColor3f(1.0, 0.0, 0.0);

    // Rectangle draw
    glBegin(GL_QUADS);

    glVertex2f(-0.2, 0.2);
    glVertex2f(0.2, 0.2);
    glVertex2f(0.2, -0.2);
    glVertex2f(-0.2, -0.2);

    glEnd();

    // আগের transformation-এ ফিরে যাওয়া
    glPopMatrix();

    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);

    glutInitWindowSize(800, 600);

    glutCreateWindow("Scaling");

    // Background Color
    glClearColor(1.0, 1.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

# 5. সবচেয়ে Important Line

```cpp
glScalef(2.0, 2.0, 1.0);
```

এখানে:

```text
2.0 → X direction-এ 2 গুণ

2.0 → Y direction-এ 2 গুণ

1.0 → Z direction-এ কোনো change নেই
```

তাই object:

```text
Width  → 2 গুণ
Height → 2 গুণ
```

বড় হবে।

---


# 6. `glScalef()`-এর 3টি Parameter

Function:

```cpp
glScalef(Sx, Sy, Sz);
```

এখানে:

```text
1st → X-axis scaling

2nd → Y-axis scaling

3rd → Z-axis scaling
```

2D-এর জন্য:

```text
Sz = 1.0
```

রাখি।

---

# 7. Scaling Factor কী?

Scaling-এর value-কে Scaling Factor বলা যায়।

যেমন:

```cpp
glScalef(2.0, 2.0, 1.0);
```

এখানে:

```text
X factor = 2
Y factor = 2
```

মানে দুই direction-এই object 2 গুণ হবে।

---


# 8. Factor = 1 হলে কী হয়?

```cpp
glScalef(1.0, 1.0, 1.0);
```

তাহলে:

```text
X → 1 গুণ
Y → 1 গুণ
```

অর্থাৎ:

> কোনো size change হবে না।

---

# 9. Factor > 1 হলে

যেমন:

```cpp
glScalef(2.0, 2.0, 1.0);
```

তাহলে:

```text
2 > 1
```

তাই object বড় হবে।

```text
1.0 → Same Size
2.0 → Bigger
3.0 → আরও Bigger
```

---


# 10. Factor < 1 হলে

যেমন:

```cpp
glScalef(0.5, 0.5, 1.0);
```

তাহলে:

```text
0.5 < 1
```

তাই object ছোট হবে।

```text
1.0 → Same
0.5 → Half
0.25 → আরও ছোট
```

---

# 11. Factor = 0 হলে

```cpp
glScalef(0.0, 0.0, 1.0);
```

এতে X এবং Y direction-এর size zero হয়ে যাবে।

অর্থাৎ object দেখা যাবে না/degenerate হয়ে যাবে।

তাই basic scaling-এ `0` avoid করাই ভালো।

---

# 12. X এবং Y একই হলে

```cpp
glScalef(2.0, 2.0, 1.0);
```

X এবং Y একই factor।

তাই:

```text
Width  → 2 গুণ
Height → 2 গুণ
```

Object-এর overall proportion একই থাকবে।

এটাকে **Uniform Scaling** বলা হয়।

---
# 13. Uniform Scaling

যখন:

```text
Sx = Sy
```

তখন Uniform Scaling।

Example:

```cpp
glScalef(2.0, 2.0, 1.0);
```

মানে:

```text
X = 2
Y = 2
```

দুই দিকেই সমানভাবে বড় হবে।

---

# 14. Non-Uniform Scaling

যখন:

```text
Sx ≠ Sy
```

তখন Non-Uniform Scaling।

Example:

```cpp
glScalef(2.0, 1.0, 1.0);
```

এখানে:

```text
X → 2 গুণ
Y → 1 গুণ
```

তাই object শুধু width-এর দিকে বড় হবে।

---

# 15. Diagram দিয়ে বুঝি

### Original:

```text
┌────┐
│    │
└────┘
```

### `glScalef(2,2,1)`:

```text
┌────────┐
│        │
│        │
└────────┘
```

দুই direction-এই বড় হয়েছে।

---

# 16. শুধু Width বাড়াতে চাইলে

```cpp
glScalef(2.0, 1.0, 1.0);
```

মানে:

```text
X → 2 গুণ
Y → Same
```

তাই:

```text
┌───────┐
│       │
└───────┘
```

এরকম wide হবে।

---

# 17. শুধু Height বাড়াতে চাইলে

```cpp
glScalef(1.0, 2.0, 1.0);
```

মানে:

```text
X → Same
Y → 2 গুণ
```

তাই object tall হবে।

---


# 18. Object ছোট করতে চাইলে

```cpp
glScalef(0.5, 0.5, 1.0);
```

মানে:

```text
Width  → Half
Height → Half
```

---


# 19. Object 3 গুণ বড় করতে চাইলে

```cpp
glScalef(3.0, 3.0, 1.0);
```

মানে:

```text
X → 3 গুণ
Y → 3 গুণ
```

---


# 20. X Direction-এ 3 গুণ এবং Y Direction-এ 2 গুণ

```cpp
glScalef(3.0, 2.0, 1.0);
```

মানে:

```text
Width  → 3 গুণ
Height → 2 গুণ
```

এটা Non-Uniform Scaling।

---

# 21. Scaling-এর Formula

যদি কোনো point:

```text
(x, y)
```

হয় এবং scaling:

```text
Sx, Sy
```

হয়, তাহলে:

```text
x' = x × Sx

y' = y × Sy
```

---

# 22. Simple Example

ধরি:

```text
Point = (0.2, 0.3)
```

Scaling:

```text
Sx = 2
Sy = 2
```

তাহলে:

```text
x' = 0.2 × 2
   = 0.4

y' = 0.3 × 2
   = 0.6
```

New Point:

```text
(0.4, 0.6)
```

অর্থাৎ point origin থেকে আরও দূরে চলে গেছে।

---


# 23. Rectangle-এর ক্ষেত্রে

ধরি Rectangle:

```text
(-0.2, 0.2)
(0.2, 0.2)
(0.2,-0.2)
(-0.2,-0.2)
```

Scaling:

```text
glScalef(2.0, 2.0, 1.0);
```

তাহলে:

```text
X coordinates → 2 গুণ
Y coordinates → 2 গুণ
```

নতুন Rectangle হবে:

```text
(-0.4, 0.4)
(0.4, 0.4)
(0.4,-0.4)
(-0.4,-0.4)
```

তাই Rectangle বড় হবে।

---

# 24. Scaling করলে Position-ও কেন Change মনে হয়?

এটা একটা important point।

Scaling formula:

```text
x' = x × Sx
y' = y × Sy
```

তাই origin থেকে দূরের point আরও দূরে যায়।

কিন্তু আসল transformation হলো:

> Object-এর size change হচ্ছে।

যদি object origin-এর center-এ থাকে, scaling দেখতে সুন্দর এবং সহজ হয়।

---

# 25. Scaling সাধারণত কোথাকে কেন্দ্র করে হয়?

Basic OpenGL scaling সাধারণত:

```text
Origin = (0,0)
```

কে reference ধরে।

```text
       +Y
        ↑
        |
        |
--------●--------→ +X
       (0,0)
```

তাই object যদি origin-এর center-এ থাকে, scaling সহজে বোঝা যায়।

---


# 26. Object Center-এ না থাকলে

ধরি object:

```text
Right side
```

এ আছে।

Scaling করলে object-এর points origin থেকে দূরে/কাছে যেতে পারে।

ফলে মনে হতে পারে object position-ও change করছে।

কিন্তু আসলে scaling origin-এর reference-এ হচ্ছে।

---

# 27. নির্দিষ্ট Center-এর চারপাশে Scaling

যদি কোনো object-এর নিজের center:

```text
(cx, cy)
```

হয়, তাহলে সাধারণ concept:

```text
1. Object-এর center-এ যাও
2. Scale করো
3. আগের জায়গায় ফিরে আসো
```

Structure:

```cpp
glPushMatrix();

glTranslatef(cx, cy, 0.0);

glScalef(2.0, 2.0, 1.0);

glTranslatef(-cx, -cy, 0.0);

// Draw Object

glPopMatrix();
```

এটা একটু advanced। Basic exam-এ শুধু `glScalef()` চাইলেই সাধারণত এটুকুই যথেষ্ট:

```cpp
glScalef(2.0, 2.0, 1.0);
```

---

# 28. `glPushMatrix()` কেন ব্যবহার করি?

আমরা লিখতে পারি:

```cpp
glPushMatrix();

glScalef(2.0, 2.0, 1.0);

// Draw Object

glPopMatrix();
```

`glPushMatrix()`:

> বর্তমান transformation state save করে।

---

# 29. `glPopMatrix()` কী করে?

```cpp
glPopMatrix();
```

আগের saved transformation state-এ ফিরে যায়।

সহজভাবে:

```text
Push → Save
Pop  → Restore
```

---

# 30. Multiple Object-এর ক্ষেত্রে

ধরি:

```text
Object 1 → বড়
Object 2 → ছোট
```

তাহলে:

```cpp
// Object 1
glPushMatrix();

glScalef(2.0, 2.0, 1.0);

// Draw Object 1

glPopMatrix();


// Object 2
glPushMatrix();

glScalef(0.5, 0.5, 1.0);

// Draw Object 2

glPopMatrix();
```

এতে দুই object আলাদাভাবে scale হবে।

---

# 31. কেন Push/Pop দরকার?

ধরি:

```cpp
glScalef(2.0, 2.0, 1.0);
```

করলাম।

তারপর আরেকটা object draw করলাম।

দ্বিতীয় object-ও এই scaling-এর effect পেতে পারে।

তাই:

```text
Push
 ↓
Scale
 ↓
Draw Object
 ↓
Pop
```

ব্যবহার করি।

---



# 33. Scaling এবং Rotation

### Rotation:

```cpp
glRotatef(45, 0, 0, 1);
```

মানে:

```text
Object → Rotate
```

### Scaling:

```cpp
glScalef(2, 2, 1);
```

মানে:

```text
Object → Bigger
```

---

# 34. Transformation তিনটা একসাথে

OpenGL-এ তিনটা একসাথে করা যায়:

```cpp
glPushMatrix();

glTranslatef(0.4, 0.2, 0.0);

glRotatef(45, 0.0, 0.0, 1.0);

glScalef(2.0, 2.0, 1.0);

// Draw Object

glPopMatrix();
```

এখানে:

```text
Translation → Move
Rotation    → Rotate
Scaling     → Bigger
```

---


# 35. Scaling-এর Main Code

Exam-এর জন্য সবচেয়ে important:

```cpp
glPushMatrix();

// Object 2 গুণ বড়
glScalef(2.0, 2.0, 1.0);

// Draw Object

glPopMatrix();
```

---

# 36. Scaling Factor মনে রাখার Trick

```text
Factor > 1
     ↓
Bigger

Factor = 1
     ↓
Same

0 < Factor < 1
     ↓
Smaller
```

উদাহরণ:

```text
2.0 → বড়
1.0 → একই
0.5 → ছোট
0.2 → আরও ছোট
```

---

# 37. Exam-এ কীভাবে চিনবে?

Question:

> **Scale the rectangle 2 times**

তাহলে:

```cpp
glScalef(2.0, 2.0, 1.0);
```

---

Question:

> **Make the object half size**

তাহলে:

```cpp
glScalef(0.5, 0.5, 1.0);
```

---

Question:

> **Increase width only**

তাহলে:

```cpp
glScalef(2.0, 1.0, 1.0);
```

---

Question:

> **Increase height only**

তাহলে:

```cpp
glScalef(1.0, 2.0, 1.0);
```

---

# 38. Viva Questions

### Q1. Scaling কী?

**Answer:** Object-এর size বড় বা ছোট করাকে Scaling বলে।

---

### Q2. OpenGL-এ Scaling-এর function কী?

**Answer:**

```cpp
glScalef()
```

---

### Q3. `glScalef()`-এ কয়টি parameter?

**Answer:** 3টি।

```text
Sx, Sy, Sz
```

---

### Q4. `Sx` কী?

**Answer:** X-axis বরাবর scaling factor।

---

### Q5. `Sy` কী?

**Answer:** Y-axis বরাবর scaling factor।

---

### Q6. 2D graphics-এ `Sz` কত রাখি?

**Answer:**

```text
1.0
```

---

### Q7. Factor `2.0` দিলে কী হবে?

**Answer:** Object 2 গুণ বড় হবে।

---

### Q8. Factor `0.5` দিলে কী হবে?

**Answer:** Object অর্ধেক ছোট হবে।

---

### Q9. Factor `1.0` দিলে কী হবে?

**Answer:** Size অপরিবর্তিত থাকবে।

---

### Q10. `Sx = Sy` হলে কী ধরনের Scaling?

**Answer:** Uniform Scaling।

---

### Q11. `Sx ≠ Sy` হলে?

**Answer:** Non-Uniform Scaling।

---

### Q12. Scaling করলে কী change হয়?

**Answer:** Object-এর size change হয়।

---

### Q13. `glPushMatrix()` কেন ব্যবহার করি?

**Answer:** Transformation state save করার জন্য।

---

### Q14. `glPopMatrix()` কেন?

**Answer:** Previous transformation state restore করার জন্য।

---


# 39. Common Mistakes

### Mistake 1: `glScale()` লেখা

ভুল:

```cpp
glScale(2, 2, 1);
```

সঠিক:

```cpp
glScalef(2, 2, 1);
```

Function-এর শেষে `f` আছে।

---

### Mistake 2: X এবং Y ভুল করা

```cpp
glScalef(2.0, 1.0, 1.0);
```

মানে:

```text
X → 2 গুণ
Y → Same
```

আর:

```cpp
glScalef(1.0, 2.0, 1.0);
```

মানে:

```text
X → Same
Y → 2 গুণ
```

---

### Mistake 3: 2D-তে Z ভুলে যাওয়া

Basic 2D scaling:

```cpp
glScalef(Sx, Sy, 1.0);
```

শেষে:

```text
1.0 → Z
```

---

### Mistake 4: Transformation-এর আগে Object draw করা

সঠিক order:

```cpp
glPushMatrix();

glScalef(2.0, 2.0, 1.0);

// তারপর Object draw

glPopMatrix();
```

অর্থাৎ:

> **আগে Scaling, তারপর Drawing।**

---

# 40. Quick Revision

```text
Scaling
   ↓
Size Change
```

Function:

```cpp
glScalef(Sx, Sy, Sz);
```

2D:

```cpp
glScalef(Sx, Sy, 1.0);
```

Factor:

```text
> 1 → Bigger

= 1 → Same

< 1 → Smaller
```

Uniform:

```text
Sx = Sy
```

Non-Uniform:

```text
Sx ≠ Sy
```

Formula:

```text
x' = x × Sx

y' = y × Sy
```

---


# 41. Three Transformations — Final Revision

| Transformation | Function         | Main কাজ           |
| -------------- | ---------------- | ------------------ |
| Translation    | `glTranslatef()` | Object Move        |
| Rotation       | `glRotatef()`    | Object Rotate      |
| Scaling        | `glScalef()`     | Object Size Change |

মনে রাখবে:

```text
T → Translate → Move
R → Rotate → Turn
S → Scale → Size
```

---


# 42. One-Line Memory Trick

> **Scaling = Object-এর size বড়/ছোট করা; `glScalef(Sx,Sy,1)`; Factor > 1 হলে বড়, 0–1 হলে ছোট, 1 হলে same।**
