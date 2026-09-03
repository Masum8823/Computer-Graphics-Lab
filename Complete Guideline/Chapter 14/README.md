# Draw a Stickman

> Stickman হলো কয়েকটি basic shape/line একসাথে ব্যবহার করে বানানো একটি simple human figure।

---

# 1. Stickman কীভাবে বানাবো?

একটা Stickman বানাতে মূলত:

```text
Circle → Head

Line → Body

Line → দুই হাত

Line → দুই পা
```

অর্থাৎ:

```text id="t7s4xk"
       Circle
         ↓
        Head

         |
         |
         |
        Body

      /     \
     /       \
   Arms

     /   \
    /     \
  Legs
```

এখানে আমরা **Circle + Lines** ব্যবহার করবো।

---


# 2. আমাদের Stickman

আমাদের Stickman-এর structure:

```text id="n7h1pz"
       O
       |
    ---|---
       |
      / \
     /   \
```

এখানে:

```text id="v2j5kk"
 O      → Head
 |      → Body
---     → Arms
/ \     → Legs
```

---