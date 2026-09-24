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