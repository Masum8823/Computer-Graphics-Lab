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


---
</details>

<details>
    <summary><b>OpenGL Lines</b></summary>


---
</details>

<details>
    <summary><b>OpenGL Triangles</b></summary>


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


