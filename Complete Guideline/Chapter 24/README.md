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
