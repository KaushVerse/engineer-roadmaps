# 🚀 C Language – **All Data Types Deep Dive** (Hinglish)

> 📄 **README.md**
> Is guide me **C language ke saare data types** ko **real-life stories, examples, memory view, code snippets, interview tips** ke saath explain kiya gaya hai. Ye beginner se leke advanced tak sab ke liye hai 🔥

---

## 🤔 Data Type hota kya hai?

👉 **Data Type** compiler ko batata hai:

* 🧠 memory kitni allocate karni hai
* 📦 data ka type kya hai
* ⚙️ operations kaise honge

📌 **Simple line:**

> *Data type = data + memory + rules*

---

# 🧒 REAL LIFE STORY (Foundation)

Socho tum **grocery store** ke owner ho 🏪

| Item            | Example   | Data Type |
| --------------- | --------- | --------- |
| Biscuit packets | 5         | `int`     |
| Milk quantity   | 1.5 litre | `float`   |
| Customer name   | "Rahul"   | `char[]`  |
| Yes / No        | true      | `bool`    |
| Locker key      | Address   | `pointer` |

👉 Jaise har item ka **alag container** hota hai, waise hi C me har data ka **alag data type** hota hai.

---

# 🧩 BASIC DATA TYPES

## 🔢 `int` – Integer

📖 **Story:**
Tumhare class me **students count** = 42

```c
int students = 42;
```

🧠 Memory: 4 bytes (mostly)

---

## 🔤 `char` – Character

📖 **Story:**
Grade = 'A'

```c
char grade = 'A';
```

🧠 Memory: 1 byte

⚠️ Single quotes mandatory

---

## 🌊 `float` – Decimal Value

📖 **Story:**
Petrol price = 104.75

```c
float petrol = 104.75f;
```

🧠 Memory: 4 bytes

---

## 🌐 `double` – High Precision Decimal

📖 **Story:**
Scientific calculation / Bank interest

```c
double interest = 7.345678;
```

🧠 Memory: 8 bytes

---

# 🧠 TYPE MODIFIERS (Power Boost 💪)

## ➕ `short`

📖 **Story:**
Age of kid = 5

```c
short age = 5;
```

---

## ➕ `long`

📖 **Story:**
Population of India

```c
long population = 1400000000;
```

---

## 🔒 `unsigned`

📖 **Story:**
ATM cash count (negative nahi hota)

```c
unsigned int cash = 50000;
```

---

# 🧵 DERIVED DATA TYPES

## 🧶 Array

📖 **Story:**
Students ke marks list

```c
int marks[5] = {90, 85, 70, 88, 92};
```

---

## 🧷 Pointer

📖 **Story:**
Ghar ka address vs ghar

```c
int x = 10;
int *p = &x;
```

👉 Pointer value nahi, **address** rakhta hai

---

## 🏗 Structure (`struct`)

📖 **Story:**
Student ka full record

```c
struct Student {
    int id;
    char name[20];
    float marks;
};
```

---

## 🎭 Union

📖 **Story:**
Ek hi room – kabhi bed, kabhi sofa

```c
union Data {
    int i;
    float f;
};
```

👉 Memory share hoti hai

---

# 🎯 USER DEFINED DATA TYPES

## 🏷 `typedef`

📖 **Story:**
Long naam ka nickname

```c
typedef unsigned long ulong;
ulong population;
```

---

## 🚦 `enum`

📖 **Story:**
Traffic signal

```c
enum Signal { RED, YELLOW, GREEN };
```

---

# 🧠 SPECIAL DATA TYPES

## 🧠 `void`

📖 **Story:**
Function kuch return nahi karta

```c
void greet() {
    printf("Hello");
}
```

---

## ✅ `_Bool` / `bool`

📖 **Story:**
Light ON / OFF

```c
#include <stdbool.h>
bool isOn = true;
```

---

# 🧪 COMPLETE REAL LIFE DEMO PROGRAM

```c
#include <stdio.h>
#include <stdbool.h>

struct Employee {
    int id;
    char name[20];
    float salary;
    bool isPermanent;
};

int main() {
    struct Employee e1 = {1, "Amit", 55000.50, true};

    printf("ID: %d\n", e1.id);
    printf("Name: %s\n", e1.name);
    printf("Salary: %.2f\n", e1.salary);
    printf("Permanent: %d\n", e1.isPermanent);

    return 0;
}
```

---

# ❌ COMMON MISTAKES (Interview Gold 🥇)

❌ `char` for string
❌ `float` instead of `double` in precision work
❌ Pointer without initialization
❌ Using union like struct

---

# 🏁 SUMMARY

✅ Data type = memory + rules
✅ Correct data type = optimized program
✅ Wrong data type = bugs + crash

---

## 🔥 Bro Tip

> **Agar tum data types samajh gaye, to C language tumhari jeb me hai** 😎💻

---

📌 **Happy Coding – C Language Mastery Begins Here 🚀**
