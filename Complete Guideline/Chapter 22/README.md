# Homogeneous Transformation

> Homogeneous Transformation হলো **2D/3D transformation-কে matrix-এর মাধ্যমে represent করার একটি পদ্ধতি**।

---

# 1. Homogeneous Transformation কী?

আমরা আগের ৩টা Transformation দেখেছি:

```text
Translation → Move
Rotation    → Rotate
Scaling     → Size Change
```

কিন্তু একটা সমস্যা আছে।

Translation-এর formula:

```text
x' = x + Tx
y' = y + Ty
```

এখানে `+` আছে।

অন্যদিকে Scaling:

```text
x' = x × Sx
y' = y × Sy
```

এখানে `×` আছে।

Rotation-এর formula-তেও `sin` এবং `cos` আছে।

এগুলোকে **একটা common matrix format**-এ আনার জন্য আমরা **Homogeneous Coordinates** ব্যবহার করি।

---
