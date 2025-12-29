# 📦 C Language – **ALL Operators Complete Guide** (Real Life + Tables | Hinglish)

> 📄 **README.md**
> Ye guide **C language ke har ek operator** ko cover karta hai – **ek bhi miss nahi** ❌
> Saath me **real-life stories**, **tables**, **examples**, **interview traps**, aur **best practices** 🔥

---

## 🤔 Operator kya hota hai?

👉 **Operator** wo symbol hota hai jo operands (data) pe **operation** karta hai.

📌 Simple line:

> *Operator = kaam karne ka tareeka*

---

# 🧠 REAL LIFE FOUNDATION STORY

Socho tum **bank account** manage kar rahe ho 🏦

* Paisa add ➕ (Arithmetic)
* Compare balance ⚖️ (Relational)
* ATM rules check 🚦 (Logical)
* Account settings toggle 🔁 (Bitwise)
* Value assign 📝 (Assignment)

➡️ Ye sab C ke operators hi karte hain.

---

# 1️⃣ 🔢 ARITHMETIC OPERATORS

| Operator | Meaning        | Real Life Example    |
| -------- | -------------- | -------------------- |
| `+`      | Addition       | Salary + Bonus       |
| `-`      | Subtraction    | Balance - Expense    |
| `*`      | Multiplication | Price × Quantity     |
| `/`      | Division       | Cake ÷ Friends       |
| `%`      | Modulus        | Remaining chocolates |

```c
int a = 10, b = 3;
printf("%d %d", a/b, a%b); // 3 1
```

⚠️ `%` sirf integer ke saath

---

# 2️⃣ ➕➖ UNARY OPERATORS

| Operator | Meaning     | Story          |
| -------- | ----------- | -------------- |
| `+`      | Unary plus  | Normal value   |
| `-`      | Unary minus | Negative debt  |
| `++`     | Increment   | Daily steps +1 |
| `--`     | Decrement   | Battery drain  |

```c
int x = 5;
printf("%d %d", x++, ++x);
```

---

# 3️⃣ ⚖️ RELATIONAL OPERATORS

| Operator | Meaning       | Example        |
| -------- | ------------- | -------------- |
| `==`     | Equal         | PIN match      |
| `!=`     | Not equal     | Wrong OTP      |
| `>`      | Greater than  | Age > 18       |
| `<`      | Less than     | Marks < Pass   |
| `>=`     | Greater equal | Balance enough |
| `<=`     | Less equal    | Limit check    |

```c
if(age >= 18) printf("Eligible");
```

---

# 4️⃣ 🚦 LOGICAL OPERATORS

| Operator | Meaning | Real Life      |    |            |
| -------- | ------- | -------------- | -- | ---------- |
| `&&`     | AND     | ATM card + PIN |    |            |
| `|`        |         | `|`               | OR | Cash / UPI |
| `!`      | NOT     | Not blocked    |    |            |

```c
if(card && pin) withdraw();
```

---

# 5️⃣ 🧷 BITWISE OPERATORS (🔥 Interview Favorite)

| Operator | Meaning          | Use           |                |
| -------- | ---------------- | ------------- | -------------- |
| `&`      | AND              | Masking       |                |
| `        | `                | OR            | Permission add |
| `^`      | XOR              | Toggle        |                |
| `~`      | One’s complement | Flip bits     |                |
| `<<`     | Left shift       | Multiply by 2 |                |
| `>>`     | Right shift      | Divide by 2   |                |

```c
int x = 5; // 0101
printf("%d", x << 1); // 10
```

---

# 6️⃣ 📝 ASSIGNMENT OPERATORS

| Operator | Example | Meaning |
| -------- | ------- | ------- |
| `=`      | a = 5   | Assign  |
| `+=`     | a += 2  | a = a+2 |
| `-=`     | a -= 2  | a = a-2 |
| `*=`     | a *= 2  | a = a*2 |
| `/=`     | a /= 2  | a = a/2 |
| `%=`     | a %= 2  | a = a%2 |

---

# 7️⃣ ❓ CONDITIONAL (TERNARY) OPERATOR

📖 Story:
Driving allowed? Age ≥ 18

```c
result = (age >= 18) ? "Yes" : "No";
```

---

# 8️⃣ 🧠 SPECIAL OPERATORS

## 📏 `sizeof`

```c
printf("%zu", sizeof(int));
```

📖 Story: Suit size before buying 👕

---

## 🧷 `,` (Comma Operator)

```c
int a = (1, 2, 3);
```

➡️ Last value assign hoti hai

---

## 🏷 `&` (Address-of)

```c
int x;
printf("%p", &x);
```

---

## 📍 `*` (Dereference)

```c
int *p = &x;
printf("%d", *p);
```

---

## 🧩 `.` and `->`

```c
s.age;    // struct
p->age;   // pointer to struct
```

---

# 9️⃣ 🔄 TYPE CASTING OPERATOR

📖 Story:
Integer ko decimal banana

```c
int a = 5;
float b = (float)a;
```

---

# 🔢 OPERATOR PRECEDENCE (Mini Table)

| Priority | Operators   |   |   |
| -------- | ----------- | - | - |
| High     | `() ++ --`  |   |   |
|          | `* / %`     |   |   |
|          | `+ -`       |   |   |
|          | `< > <= >=` |   |   |
|          | `== !=`     |   |   |
|          | `&&`        |   |   |
|          | `           |   | ` |
| Low      | `= ,`       |   |   |

---

# ❌ COMMON MISTAKES (Interview Trap 😈)

❌ `=` instead of `==`
❌ Bitwise & vs Logical &&
❌ Using ++ twice in one statement
❌ Ignoring precedence

---

# 🧪 COMPLETE DEMO PROGRAM

```c
#include <stdio.h>

int main() {
    int a = 10, b = 3;

    printf("Add: %d\n", a + b);
    printf("Mod: %d\n", a % b);
    printf("Relational: %d\n", a > b);
    printf("Logical: %d\n", (a>b && b>0));
    printf("Bitwise: %d\n", a & b);
    printf("Ternary: %d\n", (a>b)?a:b);
    printf("Size: %zu\n", sizeof(a));

    return 0;
}
```

---

# 🏁 SUMMARY

✅ All operator categories covered
✅ Real-life clarity
✅ Interview ready

---

## 🔥 Bro Tip

> **Operator clear = logic crystal clear** 🧠💎

📌 Happy Coding 🚀
