# FreeGLUT Setup in Code::Blocks 20.03

## Downloads

| Software | Link |
|----------|------|
| FreeGLUT | [Download FreeGLUT](https://drive.google.com/file/d/1oi2SXxwNzrbYf46qUGQMqwbwMYp2In26/view?usp=drive_link) |
| Code::Blocks 20.03 | [Download Code::Blocks](https://drive.google.com/file/d/1O0MrluQ-MWPRFuhCFf7NjiWsAZbZHjDo/view?usp=drive_link) |

> [!IMPORTANT]
>
> **শুরু করার আগে:**
>
> - Code::Blocks 20.03 download করো, 
> - FreeGLUT folder extract করো
> - **Notepad++** download ও install করো
>
> তারপর নিচের steps follow করো।

---

## Step 1 — Code::Blocks Install

- Existing Code::Blocks uninstall করে **Code::Blocks 20.03** browser থেকে install করতে হবে
- Destination folder same রাখতে হবে

```text
C:\Program Files\Codeblocks
```

---

## Step 2 — FreeGLUT Folder থেকে Files Copy

### Include Files

- FreeGLUT folder → `include` → `GL` → **4টি file copy**
- Paste:

```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32\include\GL
```

### Lib Files (32-bit)

- FreeGLUT → `lib` → **2টি file copy**
- Paste:

```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32\lib
```

### Lib Files (64-bit)

- FreeGLUT → `lib` → `x64` → **2টি file copy**
- Same জায়গায় paste করতে হবে

### Bin Files

- FreeGLUT → `bin` → `x64` → **3টি file copy**
- Paste:

```text
C:\Windows
```

---

## Step 3 — `glut.cbp` Template File Edit

- Navigate to:

```text
C:\Program Files\Codeblocks\Share\Codeblocks\templates
```

- Open `glut.cbp`
- File-এ **Right Click** → **Edit with Notepad++**
- `Search` → `Find & Replace`

| Option | Value |
|----------|----------|
| Find what | `glut32` |
| Replace with | `freeglut` |

- **Replace All**
- File **Save**

---

## Step 4 — `wizard.script` File Edit

- Navigate to:

```text
C:\Program Files\Codeblocks\Share\Codeblocks\templates\wizard\glut
```

- Open `wizard.script`
- File-এ **Right Click** → **Edit with Notepad++**
- `Search` → `Find & Replace`

| Option | Value |
|----------|----------|
| Find what | `glut32` |
| Replace with | `freeglut` |

- **Replace All**
- File **Save**

---

## Step 5 — New Project তৈরি

```text
Code::Blocks
    └── New Project
            └── GLUT Project
```

- Click **Next**
- **Project title** দিতে হবে
- Destination ইচ্ছামতো দেওয়া যাবে
- Click **Next**

### Destination Set

Select:

```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32
```

Then:

```text
Next → Finish
```

---

## Step 6 — Check / Verify

Navigate to:

```text
Settings → Compiler → Toolchain Executables
```

### Path

```text
C:\Program Files\Codeblocks\Mingw
```

> [!TIP]
>
> সব ঠিক থাকলে **All Clear ✓**

---

## Setup Complete

FreeGLUT is now ready to use with **Code::Blocks 20.03**.