# DDA Line Drawing Algorithm

> **DDA = Digital Differential Analyzer**

DDA হলো computer graphics-এ **দুটি point-এর মধ্যে একটি straight line draw করার algorithm**।

---

# 1. DDA কী করে?

ধরি আমাদের দুইটা point আছে:

```text
Start Point → (x1, y1)

End Point   → (x2, y2)
```

DDA algorithm এই দুই point-এর মাঝখানে ছোট ছোট step নিয়ে:

```text
Point → Point → Point → Point → Point
```

draw করে।

এই অনেকগুলো ছোট ছোট point একসাথে দেখলে আমাদের কাছে একটা **straight line** মনে হয়।

---
# 2. Example

ধরি:

```text
Start = (2,2)

End = (8,5)
```

DDA:

```text
(2,2)
   ↓
(3,2.5)
   ↓
(4,3)
   ↓
(5,3.5)
   ↓
...
   ↓
(8,5)
```

এই pointগুলোকে plot করলে line তৈরি হবে।

---

# 3. DDA-এর Main Formula

প্রথমে:

```text
dx = x2 - x1

dy = y2 - y1
```

তারপর:

```text
steps = max(|dx|, |dy|)
```

তারপর:

```text
xIncrement = dx / steps

yIncrement = dy / steps
```

তারপর:

```text
x = x1
y = y1
```

প্রতিবার:

```text
x = x + xIncrement

y = y + yIncrement
```

এবং point plot করি।

---