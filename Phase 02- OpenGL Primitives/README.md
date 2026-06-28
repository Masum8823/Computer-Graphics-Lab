<h1 align="center">OpenGL Primitives</h1>

> OpenGL Primitive is the basic drawing object used to create graphics.

### 📝 Topics Covered
- [x] Window Setup & Background
- [x] Drawing Primitives (Point, Line, Triangle)
- [x] Drawing Basic Shapes(Rectangle, Circle)



<p align="center">
  ⬇<b> Click any section below to expand </b> ⬇
</p>


<details>
    <summary><b>Window Creation & Background Color</b></summary>

# Window Creation & Background Color

## Overview

Before drawing any object in OpenGL, we must create a window and set a background color. FreeGLUT provides simple functions to initialize OpenGL, create a window, and display graphics.

---

## Program Flow

```text
Start Program
      │
      ▼
Initialize FreeGLUT
      │
      ▼
Set Window Size
      │
      ▼
Create Window
      │
      ▼
Set Background Color
      │
      ▼
Register Display Function
      │
      ▼
Start Main Event Loop
```

---

## Complete Code

```cpp
#include <GL/glut.h>

void display()
{
    glClear(GL_COLOR_BUFFER_BIT);
    glFlush();
}

int main(int argc, char** argv)
{
    glutInit(&argc, argv);
    glutInitWindowSize(800,600);
    glutCreateWindow("OpenGL Lab");
    glClearColor(0.0,0.0,1.0,1.0);
    glutDisplayFunc(display);
    glutMainLoop();

    return 0;
}
```

---

# Code Explanation

### `#include <GL/glut.h>`

Includes the FreeGLUT/OpenGL library so we can use OpenGL functions.

---

### `void display()`

This is the display callback function. OpenGL calls this function whenever the window needs to be drawn or refreshed.

---

### `glClear(GL_COLOR_BUFFER_BIT);`

Clears the window using the current background color.

* `GL_COLOR_BUFFER_BIT` → Clears the color buffer (screen).

---

### `glFlush();`

Executes all pending OpenGL commands immediately and displays the output.

---

### `glutInit(&argc, argv);`

Initializes the FreeGLUT library.

This function **must be called first** before using any other GLUT function.

---

### `glutInitWindowSize(800,600);`

Creates a window of:

* Width = **800 pixels**
* Height = **600 pixels**

---

### `glutCreateWindow("OpenGL Lab");`

Creates a window with the title:

```
OpenGL Lab
```

---

### `glClearColor(0.0,0.0,1.0,1.0);`

Sets the background color.

Format:

```cpp
glClearColor(R, G, B, Alpha);
```

Where:

* **R** = Red
* **G** = Green
* **B** = Blue
* **Alpha** = Opacity (1.0 = Fully visible)

Example:

| Color  | RGB Values |
| ------ | ---------- |
| Black  | (0,0,0)    |
| White  | (1,1,1)    |
| Red    | (1,0,0)    |
| Green  | (0,1,0)    |
| Blue   | (0,0,1)    |
| Yellow | (1,1,0)    |

In this program:

```cpp
glClearColor(0.0,0.0,1.0,1.0);
```

The window background becomes **Blue**.

---

### `glutDisplayFunc(display);`

Registers the `display()` function as the display callback.

Whenever the window needs to be drawn, OpenGL automatically calls this function.

---

### `glutMainLoop();`

Starts the GLUT event loop.

The program keeps running and waits for events such as:

* Window display
* Keyboard input
* Mouse input
* Window resize

Without this function, the window will close immediately.

---

## Output

* A window of size **800 × 600** is created.
* The window title is **OpenGL Lab**.
* The background color is **Blue**.

---

## Important Functions

| Function               | Purpose                   |
| ---------------------- | ------------------------- |
| `glutInit()`           | Initialize FreeGLUT       |
| `glutInitWindowSize()` | Set window size           |
| `glutCreateWindow()`   | Create a window           |
| `glClearColor()`       | Set background color      |
| `glutDisplayFunc()`    | Register display function |
| `glClear()`            | Clear the screen          |
| `glFlush()`            | Execute OpenGL commands   |
| `glutMainLoop()`       | Start the event loop      |

---

## Exam Tips

* `glutInit()` must be called before other GLUT functions.
* `glClearColor()` only sets the background color; `glClear()` applies it to the window.
* `glFlush()` ensures all drawing commands are executed.
* `glutMainLoop()` keeps the window open and handles events.

---
</details>

<details>
    <summary><b>OpenGL Points</b></summary>

# GL_POINTS (Drawing a Point)

## Overview

A **Point** is the simplest OpenGL primitive. It is used to draw a single dot at a specified position.

In OpenGL, points are drawn using the `GL_POINTS` primitive.

---

## Code

```cpp
glPointSize(10);

glBegin(GL_POINTS);
    glVertex2f(0.0, 0.0);
glEnd();
```

---

# Code Explanation

### `glPointSize(10);`

Sets the size of the point.

```cpp
glPointSize(size);
```

* Unit: Pixels
* Here, the point size is **10 pixels**.

---

### `glBegin(GL_POINTS);`

Starts drawing using the **Point Primitive**.

Everything between `glBegin()` and `glEnd()` is treated as point data.

---

### `glVertex2f(0.0, 0.0);`

Specifies the position of the point.

```cpp
glVertex2f(x, y);
```

* `x` → Horizontal position
* `y` → Vertical position
* `2f` means **2-dimensional floating-point coordinates**.

In this example:

```cpp
glVertex2f(0.0, 0.0);
```

The point is drawn at the **center of the window**.

---

### `glEnd();`

Ends the drawing operation.

---

# Coordinate System

OpenGL uses a normalized coordinate system.

```text
        (+Y)
          ↑
          │
(-1,0) ───┼─── (+1,0)
          │
          │
          ↓
        (-Y)
```

* Center → `(0.0, 0.0)`
* Left → `(-1.0, 0.0)`
* Right → `(1.0, 0.0)`
* Top → `(0.0, 1.0)`
* Bottom → `(0.0, -1.0)`

---

## Example Coordinates

| Coordinate     | Position    |
| -------------- | ----------- |
| `(0.0, 0.0)`   | Center      |
| `(0.5, 0.5)`   | Upper-right |
| `(-0.5, 0.5)`  | Upper-left  |
| `(0.5, -0.5)`  | Lower-right |
| `(-0.5, -0.5)` | Lower-left  |

---

## Output

The program draws:

* One point
* Size = **10 pixels**
* Position = **Center of the window**

---

## Important Functions

| Function             | Purpose                         |
| -------------------- | ------------------------------- |
| `glPointSize()`      | Sets the point size             |
| `glBegin(GL_POINTS)` | Starts drawing points           |
| `glVertex2f()`       | Specifies the point coordinates |
| `glEnd()`            | Ends the drawing operation      |

---

## Exam Tips

* `GL_POINTS` is the OpenGL primitive used to draw one or more points.
* `glPointSize()` controls the size of the point in pixels.
* `glVertex2f(x, y)` specifies the position of each point.
* Every `glBegin()` must have a matching `glEnd()`.
* The coordinate `(0.0, 0.0)` represents the **center** of the OpenGL window.

---
</details>

<details>
    <summary><b>OpenGL Lines</b></summary>

# GL_LINES (Drawing a Line)

## Overview

A **Line** is one of the basic OpenGL primitives. It is drawn by specifying **two vertices (starting point and ending point)**.

OpenGL uses the `GL_LINES` primitive to draw individual straight lines.

---

## Code

```cpp
glBegin(GL_LINES);

glVertex2f(-0.5, 0.0);
glVertex2f(0.5, 0.0);

glEnd();
```

---

# Code Explanation

### `glBegin(GL_LINES);`

Starts drawing using the **Line Primitive**.

OpenGL reads every **two vertices** as one complete line.

---

### `glVertex2f(-0.5, 0.0);`

Specifies the **starting point** of the line.

```cpp
glVertex2f(x, y);
```

* **x = -0.5**
* **y = 0.0**

This point is located on the **left side** of the window.

---

### `glVertex2f(0.5, 0.0);`

Specifies the **ending point** of the line.

* **x = 0.5**
* **y = 0.0**

This point is located on the **right side** of the window.

---

### `glEnd();`

Ends the drawing operation.

---

# How GL_LINES Works

`GL_LINES` always takes **two vertices** to create one line.

```text
Vertex 1 ───────── Vertex 2
```

If more vertices are provided:

```cpp
glBegin(GL_LINES);

glVertex2f(A);
glVertex2f(B);

glVertex2f(C);
glVertex2f(D);

glEnd();
```

OpenGL draws:

```text
A ───── B

C ───── D
```

Each pair of vertices forms a **separate line**.

---

# Coordinate Visualization

```text
          (+Y)
            ↑
            │
            │
(-0.5,0) ●────────────● (0.5,0)
            │
            │
            ↓
          (-Y)
```

The line is drawn **horizontally through the center** of the window.

---

## Output

The program draws:

* One straight line
* Starts at **(-0.5, 0.0)**
* Ends at **(0.5, 0.0)**
* Passes through the **center of the window**

---

## Important Functions

| Function            | Purpose                             |
| ------------------- | ----------------------------------- |
| `glBegin(GL_LINES)` | Starts drawing lines                |
| `glVertex2f()`      | Specifies the start/end coordinates |
| `glEnd()`           | Ends the drawing operation          |

---

## Exam Tips

* `GL_LINES` draws **one line for every two vertices**.
* The **first vertex** is the starting point, and the **second vertex** is the ending point.
* If four vertices are given, OpenGL draws **two separate lines**.
* Every `glBegin()` must have a matching `glEnd()`.

---
</details>

<details>
    <summary><b>OpenGL Triangles</b></summary>

# GL_TRIANGLES (Drawing a Triangle)

## Overview

A **Triangle** is one of the most commonly used OpenGL primitives. It is created by specifying **three vertices**, where each vertex represents one corner of the triangle.

OpenGL uses the `GL_TRIANGLES` primitive to draw individual triangles.

---

## Code

```cpp
glBegin(GL_TRIANGLES);

glColor3f(1,0,0);
glVertex2f(0.0,0.5);

glColor3f(0,1,0);
glVertex2f(-0.5,-0.5);

glColor3f(0,0,1);
glVertex2f(0.5,-0.5);

glEnd();
```

---

# Code Explanation

### `glBegin(GL_TRIANGLES);`

Starts drawing using the **Triangle Primitive**.

OpenGL takes **three vertices** to create one triangle.

---

### `glColor3f(1,0,0);`

Sets the drawing color to **Red**.

```cpp
glColor3f(R, G, B);
```

Where:

* **R** = Red
* **G** = Green
* **B** = Blue

Each value ranges from **0.0 to 1.0**.

---

### `glVertex2f(0.0,0.5);`

Specifies the **top vertex** of the triangle.

Current color: **Red**

---

### `glColor3f(0,1,0);`

Changes the drawing color to **Green**.

---

### `glVertex2f(-0.5,-0.5);`

Specifies the **bottom-left vertex**.

Current color: **Green**

---

### `glColor3f(0,0,1);`

Changes the drawing color to **Blue**.

---

### `glVertex2f(0.5,-0.5);`

Specifies the **bottom-right vertex**.

Current color: **Blue**

---

### `glEnd();`

Ends the drawing operation.

---

# How GL_TRIANGLES Works

`GL_TRIANGLES` always uses **three vertices** to draw one triangle.

```text
        A
       / \
      /   \
     /     \
    B-------C
```

* Vertex A → Top
* Vertex B → Bottom-left
* Vertex C → Bottom-right

If six vertices are provided, OpenGL draws **two separate triangles**.

---

# Color Interpolation

Each vertex has its own color.

```text
Top Vertex          → Red
Bottom Left Vertex  → Green
Bottom Right Vertex → Blue
```

OpenGL automatically **blends (interpolates)** these colors across the triangle, creating a smooth color transition.

---

# Coordinate Visualization

```text
          (0.0,0.5)
               ▲
              / \
             /   \
            /     \
           /       \
(-0.5,-0.5)──────(0.5,-0.5)
```

---

## Output

The program draws:

* One triangle
* Three vertices
* Three different colors (Red, Green, Blue)
* Smooth color blending across the triangle

---

## Important Functions

| Function                | Purpose                                  |
| ----------------------- | ---------------------------------------- |
| `glBegin(GL_TRIANGLES)` | Starts drawing triangles                 |
| `glColor3f()`           | Sets the current drawing color           |
| `glVertex2f()`          | Specifies the coordinates of each vertex |
| `glEnd()`               | Ends the drawing operation               |

---

## Common Color Values

| Color   | RGB Values |
| ------- | ---------- |
| Red     | `(1,0,0)`  |
| Green   | `(0,1,0)`  |
| Blue    | `(0,0,1)`  |
| White   | `(1,1,1)`  |
| Black   | `(0,0,0)`  |
| Yellow  | `(1,1,0)`  |
| Cyan    | `(0,1,1)`  |
| Magenta | `(1,0,1)`  |

---

## Exam Tips

* `GL_TRIANGLES` requires **3 vertices** to draw one triangle.
* Each `glVertex2f()` specifies one corner of the triangle.
* `glColor3f()` sets the color of the next vertex.
* OpenGL automatically blends the vertex colors across the triangle.
* Every `glBegin()` must have a matching `glEnd()`.

---
</details>

<details>
    <summary><b>Drawing Rectangle</b></summary>


---
</details>

<details>
    <summary><b>Drawing Circle</b></summary>


---
</details>


