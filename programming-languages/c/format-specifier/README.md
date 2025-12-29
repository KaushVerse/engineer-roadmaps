# 🔥 C Language – **All Format Specifiers Deep Dive** (Hinglish)

> 📄 **README.md** – Ye guide **C language ke saare important format specifiers** ko deep level pe explain karta hai, with **icons, tables, examples, edge-cases, aur best practices**.

---

## 📌 Format Specifier kya hota hai?

👉 **Format specifier** ek special symbol hota hai jo `printf()` / `scanf()` ko batata hai:

* data **ka type kya hai**
* data **kaise print ya read karna hai**

```c
printf("%d", x);
```

Yahan `%d` → integer ke liye format specifier hai.

---

## 🧠 Memory + Type Mapping (Important Concept)

| Data Type | Size (Typical)   | Specifier |
| --------- | ---------------- | --------- |
| `char`    | 1 byte           | `%c`      |
| `int`     | 4 bytes          | `%d`      |
| `float`   | 4 bytes          | `%f`      |
| `double`  | 8 bytes          | `%lf`     |
| `pointer` | 8 bytes (64-bit) | `%p`      |

⚠️ **Galat specifier = Undefined Behavior (UB)** 😈

---

# 🧩 INTEGER FORMAT SPECIFIERS

## 🔢 `%d` / `%i` – Signed Integer

```c
int x = -10;
printf("%d %i", x, x);
```

📝 `%d` aur `%i` almost same hain (`scanf` me thoda diff).

---

## 🔢 `%u` – Unsigned Integer

```c
unsigned int x = 10;
printf("%u", x);
```

🚫 Negative value allowed nahi hoti.

---

## 🔢 `%o` – Octal

```c
int x = 10;
printf("%o", x); // 12
```

---

## 🔢 `%x` / `%X` – Hexadecimal

```c
int x = 255;
printf("%x %X", x, x); // ff FF
```

---

# 🔤 CHARACTER & STRING

## 🅰️ `%c` – Character

```c
char ch = 'A';
printf("%c", ch);
```

---

## 🧵 `%s` – String

```c
char name[] = "Kaush";
printf("%s", name);
```

⚠️ `\0` (null terminator) hona zaroori hai.

---

# 🔣 FLOATING POINT SPECIFIERS

## 🌊 `%f` – Float / Double (printf)

```c
float a = 3.14;
double b = 2.718;
printf("%f %f", a, b);
```

📌 `printf` me **float promote hoke double ban jata hai**.

---

## 🎯 `%.nf` – Precision Control

```c
printf("%.2f", 3.14159); // 3.14
```

---

## 🌐 `%e` / `%E` – Scientific Notation

```c
printf("%e", 1234.56); // 1.234560e+03
```

---

## 🔄 `%g` / `%G` – Smart Format

```c
printf("%g", 1234.0);
```

➡️ `%f` ya `%e` me se jo short ho use karta hai.

---

# 🧮 LONG TYPES

## 🧱 `%ld` – long int

```c
long x = 100000;
printf("%ld", x);
```

## 🏗 `%lld` – long long int

```c
long long y = 9999999999;
printf("%lld", y);
```

---

# 🧷 SIZE_T & POINTERS

## 📍 `%p` – Pointer Address

```c
int x = 10;
printf("%p", (void*)&x);
```

⚠️ Always cast to `(void*)`

---

## 📏 `%zu` – size_t

```c
size_t s = sizeof(int);
printf("%zu", s);
```

---

# ⌨️ SCANF FORMAT SPECIFIERS (INPUT)

## 📥 `%d`

```c
int x;
scanf("%d", &x);
```

## 📥 `%f` vs `%lf`

```c
float a;
double b;

scanf("%f", &a);   // float
scanf("%lf", &b);  // double
```

⚠️ Ye **bahut common mistake** hai.

---

# 🎨 WIDTH, FLAGS & ALIGNMENT

## 📐 Width

```c
printf("%5d", 10); // ___10
```

## ⬅️ Left Align

```c
printf("%-5d", 10); // 10___
```

## ➕ Force Sign

```c
printf("%+d", 10); // +10
```

## 🔒 Zero Padding

```c
printf("%05d", 42); // 00042
```

---

# ❌ COMMON MISTAKES (Interview Favorite 😎)

❌ `%d` for `float`
❌ `%f` in `scanf` for `double`
❌ `%s` without allocated memory
❌ Pointer without `%p`

---

# 🧪 COMPLETE DEMO PROGRAM

```c
#include <stdio.h>

int main() {
    int i = 10;
    float f = 3.14f;
    double d = 2.718;
    char c = 'A';
    char s[] = "C Language";

    printf("int: %d\n", i);
    printf("float: %.2f\n", f);
    printf("double: %lf\n", d);
    printf("char: %c\n", c);
    printf("string: %s\n", s);
    printf("address: %p\n", (void*)&i);

    return 0;
}
```

---

# 🏁 SUMMARY

✅ Format specifier = type safety
✅ Galat specifier = crash / UB
✅ Interview + Production dono ke liye important

---

## 🚀 Tip from Bro

> **Agar tum C ke format specifiers master kar liye, to tum 50% C language already jeet gaye** 💪🔥

---

📌 **Happy Coding in C 🧠💻**
