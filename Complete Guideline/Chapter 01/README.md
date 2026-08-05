# Window Creation & Background Color

> **FreeGLUT-এর মাধ্যমে একটি Window তৈরি করা এবং তার Background Color সেট করা।**

---

## 1. কী শিখবো?

এই program থেকে আমরা শিখবো:

* FreeGLUT/OpenGL window তৈরি করা
* Window-এর size নির্ধারণ করা
* Window-এর title দেওয়া
* Background color সেট করা
* `display()` function ব্যবহার করা
* `glutMainLoop()` দিয়ে program চালু রাখা

---

## 2. Complete Code

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

    glutInitWindowSize(800, 600);

    glutCreateWindow("OpenGL Lab");

    glClearColor(0.0, 0.0, 1.0, 1.0);

    glutDisplayFunc(display);

    glutMainLoop();

    return 0;
}
```

---

## 3. Line-by-Line Explanation

### `#include <GL/glut.h>`

```cpp
#include <GL/glut.h>
```

FreeGLUT/OpenGL library program-এর সাথে যুক্ত করা হচ্ছে।

এই library-এর মাধ্যমে আমরা বিভিন্ন OpenGL/GLUT function ব্যবহার করতে পারি।

যেমন:

```text
glClear()
glFlush()
glClearColor()
glutInit()
glutCreateWindow()
glutMainLoop()
```

---

### `void display()`

```cpp
void display()
```

এটি একটি **Display Function**।

Window-এর ভিতরে যা draw বা display করতে চাই, সাধারণত এই function-এর ভিতরে লিখি।

---

### `glClear(GL_COLOR_BUFFER_BIT);`

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

Screen পরিষ্কার করে।

এখানে `GL_COLOR_BUFFER_BIT` ব্যবহার করা হয়েছে কারণ আমরা **Color Buffer** clear করতে চাই।

সহজভাবে:

> Screen পরিষ্কার করো এবং নতুন background color দেখানোর জন্য প্রস্তুত করো।

---

### `glFlush();`

```cpp
glFlush();
```

OpenGL-এর drawing command execute করে screen-এ output দেখাতে সাহায্য করে।

সহজভাবে:

> Drawing-এর কাজ screen-এ পাঠিয়ে দাও।

---

## 4. `main()` Function

```cpp
int main(int argc, char** argv)
```

C/C++ program এখান থেকে শুরু হয়।

`argc` এবং `argv` command-line arguments-এর জন্য ব্যবহৃত হয় এবং GLUT initialization-এর সময় এগুলো পাঠানো হয়।

---

### `glutInit(&argc, argv);`

```cpp
glutInit(&argc, argv);
```

GLUT/FreeGLUT initialize করে।

অর্থাৎ OpenGL window তৈরি ও ব্যবহার করার জন্য FreeGLUT environment প্রস্তুত করা হয়।

**সহজভাবে:**

> FreeGLUT চালু করো।

---

### `glutInitWindowSize(800, 600);`

```cpp
glutInitWindowSize(800, 600);
```

Window-এর size নির্ধারণ করে।

```text
Width  = 800 pixels
Height = 600 pixels
```

অর্থাৎ:

```text
          800 pixels
<---------------------------->

+----------------------------+
|                            |
|                            |
|                            |  600 pixels
|                            |
|                            |
+----------------------------+
```

---

### `glutCreateWindow("OpenGL Lab");`

```cpp
glutCreateWindow("OpenGL Lab");
```

একটি OpenGL window তৈরি করে।

Window-এর title হবে:

```text
OpenGL Lab
```

---

## 5. Background Color

### `glClearColor()`

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এই function দিয়ে background/clear color সেট করা হয়।

এর format:

```cpp
glClearColor(R, G, B, A);
```

এখানে:

```text
R = Red
G = Green
B = Blue
A = Alpha
```

আমাদের code:

```text
R = 0.0
G = 0.0
B = 1.0
A = 1.0
```

তাই color হবে:

```text
Blue
```

### মনে রাখো

```text
(1, 0, 0) → Red

(0, 1, 0) → Green

(0, 0, 1) → Blue

(1, 1, 1) → White

(0, 0, 0) → Black
```

---

## 6. Alpha কী?

`glClearColor()`-এর শেষ value হলো **Alpha**।

```cpp
glClearColor(R, G, B, A);
```

এখানে:

```text
A = Alpha
```

সাধারণভাবে:

```text
1.0 → Fully Opaque
0.0 → Fully Transparent
```

এই basic program-এ আমরা:

```cpp
A = 1.0
```

ব্যবহার করেছি।

---

## 7. `glutDisplayFunc(display);`

```cpp
glutDisplayFunc(display);
```

এখানে `display()` function-কে GLUT-এর সাথে **register** করা হচ্ছে।

এর অর্থ:

> Window-তে কিছু display/refresh করার প্রয়োজন হলে `display()` function ব্যবহার করো।

অর্থাৎ আমরা লিখেছি:

```cpp
glutDisplayFunc(display);
```

এখানে `display` হলো function-এর নাম।

---

## 8. `glutMainLoop();`

```cpp
glutMainLoop();
```

এটি program-এর main event loop চালু করে।

এটি window-কে চালু রাখে এবং বিভিন্ন event-এর জন্য অপেক্ষা করে।

যেমন:

* Window refresh
* Keyboard input
* Mouse input
* Window-related events

সহজভাবে:

> Window চালু রাখো এবং user/event-এর জন্য অপেক্ষা করো।

---

## 9. `return 0;`

```cpp
return 0;
```

Program successfully শেষ হয়েছে বোঝায়।

তবে মনে রাখবে, `glutMainLoop()` সাধারণত program-কে চলমান রাখে, তাই এই line সাধারণত immediately execute হয় না।

---

# 10. Program Execution Flow

পুরো program-টা এইভাবে কাজ করে:

```text
main()
  ↓
glutInit()
  ↓
Window Size Set
  ↓
Window Create
  ↓
Background Color Set
  ↓
display() Register
  ↓
glutMainLoop()
  ↓
display()
  ↓
glClear()
  ↓
glFlush()
  ↓
Output Show
```

---

# 11. কোন Function কী কাজ করে?

| Function               | কাজ                                |
| ---------------------- | ---------------------------------- |
| `glutInit()`           | FreeGLUT initialize করে            |
| `glutInitWindowSize()` | Window-এর size সেট করে             |
| `glutCreateWindow()`   | Window তৈরি করে                    |
| `glClearColor()`       | Clear/Background color সেট করে     |
| `glutDisplayFunc()`    | Display function register করে      |
| `glClear()`            | Buffer clear করে                   |
| `glFlush()`            | Drawing command execute/finish করে |
| `glutMainLoop()`       | Window ও event loop চালু রাখে      |

---

# 12. Important Difference

### `glClearColor()` বনাম `glClear()`

এই দুইটা খুব ভালোভাবে মনে রাখবে।

```cpp
glClearColor(0.0, 0.0, 1.0, 1.0);
```

এটি **color সেট করে**।

আর:

```cpp
glClear(GL_COLOR_BUFFER_BIT);
```

এটি **buffer clear করে এবং সেট করা clear color ব্যবহার করে**।

### সহজভাবে:

```text
glClearColor()
      ↓
কোন Color হবে সেটা সেট করে

glClear()
      ↓
Screen/Color Buffer clear করে
```

---