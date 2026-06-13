# 🎨 FreeGLUT Setup Guide for Code::Blocks 20.03

> A complete, step-by-step guide to configure FreeGLUT with Code::Blocks 20.03 on Windows

## 📋 Table of Contents
- [Prerequisites](#prerequisites)
- [Downloads](#downloads)
- [Installation Steps](#installation-steps)
  - [Step 1: Install Code::Blocks](#step-1-install-codeblocks)
  - [Step 2: Copy FreeGLUT Files](#step-2-copy-freeglut-files)
  - [Step 3: Edit GLUT Template](#step-3-edit-glut-template)
  - [Step 4: Edit Wizard Script](#step-4-edit-wizard-script)
  - [Step 5: Create New Project](#step-5-create-new-project)
  - [Step 6: Verify Installation](#step-6-verify-installation)

---

## 📦 Prerequisites

Before starting, ensure you have:

| Requirement | Description |
|-------------|-------------|
| ⚙️ **Code::Blocks 20.03** | Must be freshly installed |
| 📁 **FreeGLUT Package** | Extracted and ready |
| 📝 **Notepad++** | For editing configuration files |
| 🔑 **Administrator Rights** | Required for copying to system folders |

---

## 🔗 Downloads

| Software | Download Link | Version |
|----------|--------------|---------|
| **FreeGLUT** | [⬇️ Download FreeGLUT](https://drive.google.com/file/d/1oi2SXxwNzrbYf46qUGQMqwbwMYp2In26/view?usp=drive_link) | Latest |
| **Code::Blocks** | [⬇️ Download Code::Blocks 20.03](https://drive.google.com/file/d/1O0MrluQ-MWPRFuhCFf7NjiWsAZbZHjDo/view?usp=drive_link) | 20.03 |

> ⚠️ **Important:** Complete the prerequisites before proceeding with the installation steps below.

---

## 🚀 Installation Steps

## 1️⃣ Step 1 — Code::Blocks Install

- Existing Code::Blocks uninstall করে **Code::Blocks 20.03** install করতে হবে  
- Destination folder same রাখতে হবে →  
```text
C:\Program Files\Codeblocks
```

---

## 2️⃣ Step 2 — FreeGLUT Folder থেকে Files Copy

###  Include Files
- FreeGlut folder → `include` → `GL` → **4টি file copy**
- Paste →  
```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32\include\GL
```

---

### Lib Files (32-bit)
- FreeGlut → `lib` → **2টি file copy**
- Paste →  
```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32\lib
```

---

###  Lib Files (64-bit)
- FreeGlut → `lib` → `x64` → **2টি file copy**
- Same জায়গায় paste করতে হবে

---

###  Bin Files
- FreeGlut → `bin` → `x64` → **1টি file copy**
- Paste →  
```text
C:\Windows
```

---

## 3️⃣ Step 3 — `glut.cbp` Template File Edit

- Path:
```text
C:\Program Files\Codeblocks\Share\Codeblocks\templates
```

- `glut.cbp` → Right Click → **Edit with Notepad++**

### 🔎 Find & Replace

| Field | Value |
|------|------|
| Find what | `glut32` |
| Replace with | `freeglut` |

- Replace All → Save

---

## 4️⃣ Step 4 — `wizard.script` File Edit

- Path:
```text
C:\Program Files\Codeblocks\Share\Codeblocks\templates\wizard\glut
```

- Open `wizard.script`

### 🔎 Find & Replace

| Field | Value |
|------|------|
| Find what | `glut32` |
| Replace with | `freeglut` |

- Replace All → Save

---

## 5️⃣ Step 5 — New Project তৈরি

```
Code::Blocks
 └── New Project
      └── GLUT Project
```

- Project Title set করো  
- Destination folder choose করো  
- Next → Finish  

---

### 📂 Destination
```text
C:\Program Files\Codeblocks\Mingw\x86-64-w64-mingw32
```

---

## 6️⃣ Step 6 — Check / Verify

- Settings → Compiler → Toolchain Executables

### ✔ Path
```text
C:\Program Files\Codeblocks\Mingw
```

---

> ✅ সব ঠিক থাকলে FreeGLUT setup completed successfully!