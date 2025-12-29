# 🧱 C Language – **Memory Layout (Stack vs Heap)**

> 📄 **README.md**
> Ye guide **C program ki memory layout** ko **story-based**, **mental diagrams**, **real-life analogies**, **code examples**, aur **interview traps** ke saath explain karta hai.
> Agar ye clear ho gaya → pointers, bugs, crashes sab samajh aa jaayenge 🔥

---

## 🧠 Big Question: Program run hote hi memory me kya hota hai?

Jab C program start hota hai, OS ek **memory building** banata hai 🏢

Is building ke floors:

```
┌──────────────────┐  👑 High Address
│   Stack          │
│   (Functions)    │
├──────────────────┤
│   Heap           │
│   (Dynamic)      │
├──────────────────┤
│   BSS Segment    │
├──────────────────┤
│   Data Segment   │
├──────────────────┤
│   Text / Code    │
└──────────────────┘  👣 Low Address
```

---

# 🏢 MASTER STORY – Office Building Analogy

| Memory Part | Real Life                 |
| ----------- | ------------------------- |
| Code        | Company rules book 📘     |
| Global data | Permanent employees 🧑‍💼 |
| Stack       | Temporary workers 🧑‍🔧   |
| Heap        | Warehouse storage 📦      |

---

# 1️⃣ 🧾 TEXT / CODE SEGMENT

## 📖 Story

Company ka **rule book** – read-only 📘

```c
int add(int a, int b) {
    return a + b;
}
```

🔹 Contains compiled instructions
🔹 Read-only (mostly)

---

# 2️⃣ 📊 DATA SEGMENT

## 📖 Story

Permanent employees with ID cards 🧑‍💼

```c
int x = 10;      // initialized global
static int y = 5;
```

🔹 Initialized global & static variables

---

# 3️⃣ 📦 BSS SEGMENT

## 📖 Story

Employees hired but salary not set yet 😄

```c
int a;          // uninitialized global
static int b;
```

🔹 Auto-initialized to zero

---

# 4️⃣ 🪜 STACK MEMORY

## 📖 Story

Temporary workers – kaam khatam, bahar 🚪

```c
void fun() {
    int x = 10;
}
```

🔹 Stores:

* Local variables
* Function parameters
* Return addresses

🔹 LIFO (Last In First Out)

### ⚠️ Stack Danger

❌ Stack overflow (deep recursion)
❌ Returning address of local variable

---

# 5️⃣ 📦 HEAP MEMORY

## 📖 Story

Warehouse – jab chaaho lo, jab chaaho chhodo 📦

```c
int *p = (int*)malloc(sizeof(int));
*p = 10;
free(p);
```

🔹 Dynamic memory allocation
🔹 Programmer controlled

### ⚠️ Heap Danger

❌ Memory leak
❌ Use after free
❌ Forgetting free()

---

# ⚔️ STACK vs HEAP COMPARISON

| Feature    | Stack          | Heap       |
| ---------- | -------------- | ---------- |
| Allocation | Automatic      | Manual     |
| Speed      | Very Fast ⚡    | Slower 🐢  |
| Lifetime   | Function scope | Until free |
| Size       | Limited        | Large      |
| Control    | Compiler       | Programmer |

---

# 🧠 POINTERS & MEMORY RELATION

```c
int *p = malloc(sizeof(int));
```

📌 Pointer khud **stack** me hota hai
📌 Data **heap** me hota hai

---

# 🧪 COMPLETE MEMORY DEMO PROGRAM

```c
#include <stdio.h>
#include <stdlib.h>

int g = 10;       // Data segment
int h;            // BSS segment

void demo() {
    int x = 5;    // Stack
    int *p = malloc(sizeof(int)); // Stack + Heap

    *p = 20;
    printf("x = %d, *p = %d\n", x, *p);

    free(p);
}

int main() {
    demo();
    return 0;
}
```

---

# ❌ COMMON INTERVIEW TRAPS 😈

❌ Returning pointer to stack memory
❌ Forgetting free()
❌ Confusing stack pointer vs heap data
❌ Assuming heap auto-cleans

---

# 🏁 FINAL MENTAL MODEL

> **Stack = Temporary table**
> **Heap = Godown / warehouse**

Agar ye difference clear hai → segmentation fault se darr khatam 😎

---

## 🔥 Bro Tip

> **99% C bugs = stack & heap ka confusion** 🧠☠️

📌 Happy Coding – Memory ka Malik bano 💪🔥
