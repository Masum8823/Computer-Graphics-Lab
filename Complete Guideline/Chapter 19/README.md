# Translation

> Translation হলো কোনো object/shape-কে **এক জায়গা থেকে অন্য জায়গায় move করা**, কিন্তু shape-এর size বা angle পরিবর্তন হয় না।

---

# 1. Translation কী?

সহজ ভাষায়:

```text
Object
  ↓
Move
  ↓
New Position
```

যেমন:

```text
আগে                 পরে

  ■                    ■
                     →
```

Square-এর shape একই থাকবে, শুধু position change হবে।

---

# 2. Translation-এর Basic Formula

একটি point যদি হয়:

```text
(x, y)
```

Translation-এর পরে:

```text
x' = x + Tx
y' = y + Ty
```

এখানে:

```text
Tx = X direction-এ কতটুকু move করবে
Ty = Y direction-এ কতটুকু move করবে
```

---

# 3. সহজ Example

ধরি একটি point:

```text
(0.2, 0.3)
```

এখন:

```text
Tx = 0.4
Ty = 0.2
```

দিলে:

```text
x' = 0.2 + 0.4
   = 0.6

y' = 0.3 + 0.2
   = 0.5
```

নতুন point:

```text
(0.6, 0.5)
```

অর্থাৎ Point-টা Right এবং Up দিকে গেছে।

---

# 4. OpenGL-এ Translation

OpenGL-এ Translation করার জন্য:

```cpp
glTranslatef(Tx, Ty, 0);
```

ব্যবহার করা যায়।

এখানে:

```text
Tx → X direction
Ty → Y direction
0  → Z direction
```

আমরা 2D graphics করছি, তাই Z = `0` রাখবো।

---