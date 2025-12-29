# 🔁 C Language – **Loops & Control Flow** (Story Based | Hinglish)

> 📄 **README.md**
> Ye guide **C language ke saare loops aur control flow statements** ko **real-life stories**, **tables**, **examples**, **logic building**, aur **interview traps** ke saath explain karta hai.
> Beginner → Pro flow 🔥

---

## 🤔 Control Flow kya hota hai?

👉 **Control Flow** decide karta hai:

* code **kis order me chalega**
* **kitni baar chalega**
* **kab rukega**

📌 Simple line:

> *Program ka traffic control = Control Flow* 🚦

---

# 🧠 MASTER REAL-LIFE STORY (Big Picture)

Socho tum **Zomato delivery system** bana rahe ho 🍔🛵

* Agar payment successful → order confirm ✅ (`if`)
* Nahi to → cancel ❌ (`else`)
* Har order ke liye same steps repeat 🔁 (`loop`)
* Kabhi condition false hui → break 🛑
* Kabhi ek step skip → continue ⏭️

➡️ Ye sab **loops & control flow** se hota hai.

---

# 1️⃣ 🔀 IF STATEMENT

## 📖 Story

Agar baarish ho rahi hai ☔ → umbrella le jao

```c
if(rain) {
    takeUmbrella();
}
```

---

# 2️⃣ 🔀 IF–ELSE

## 📖 Story

Agar age ≥ 18 → vote, warna ghar jao 🗳️

```c
if(age >= 18) {
    printf("Vote allowed");
} else {
    printf("Not allowed");
}
```

---

# 3️⃣ 🔀 IF–ELSE–IF LADDER

## 📖 Story (Marks System)

```c
if(marks >= 90)
    grade = 'A';
else if(marks >= 75)
    grade = 'B';
else if(marks >= 60)
    grade = 'C';
else
    grade = 'F';
```

➡️ Multiple conditions, top-down check

---

# 4️⃣ 🎛 SWITCH–CASE

## 📖 Story

Remote ke buttons 📺

```c
switch(choice) {
    case 1: play(); break;
    case 2: pause(); break;
    case 3: stop(); break;
    default: exit();
}
```

⚠️ `break` bhool gaye → **fall-through** 😈

---

# 5️⃣ 🔁 WHILE LOOP

## 📖 Story

Jab tak phone battery > 0 📱

```c
while(battery > 0) {
    usePhone();
}
```

📌 Entry-controlled loop

---

# 6️⃣ 🔁 DO–WHILE LOOP

## 📖 Story

ATM machine – ek baar to try karega hi 🏧

```c
do {
    enterPin();
} while(pinWrong);
```

📌 Exit-controlled (runs at least once)

---

# 7️⃣ 🔁 FOR LOOP

## 📖 Story

Gym me 10 pushups 💪

```c
for(int i = 1; i <= 10; i++) {
    pushup();
}
```

📌 Best for known count loops

---

# 🧠 LOOP COMPARISON TABLE

| Loop       | Condition Check | Min Runs | Best Use           |
| ---------- | --------------- | -------- | ------------------ |
| `while`    | Start           | 0        | Unknown iterations |
| `do-while` | End             | 1        | Must run once      |
| `for`      | Start           | 0        | Fixed iterations   |

---

# 8️⃣ 🛑 BREAK STATEMENT

## 📖 Story

Fire alarm 🔥 → building exit

```c
if(fire) break;
```

➡️ Loop ya switch se bahar

---

# 9️⃣ ⏭️ CONTINUE STATEMENT

## 📖 Story

Road pe speed breaker → slow, skip nahi

```c
if(speedBreaker) continue;
```

➡️ Current iteration skip

---

# 🔁 NESTED LOOPS

## 📖 Story

School: classes ke andar students 🏫

```c
for(int c = 1; c <= 3; c++) {
    for(int s = 1; s <= 5; s++) {
        printf("Class %d Student %d\n", c, s);
    }
}
```

---

# 1️⃣0️⃣ 🚪 GOTO (⚠️ Dangerous)

## 📖 Story

Direct jump like teleportation 🌀

```c
goto end;

end:
    printf("Done");
```

⚠️ Avoid in real projects

---

# 🧪 COMPLETE REAL-LIFE DEMO PROGRAM

```c
#include <stdio.h>

int main() {
    int orders = 3;

    for(int i = 1; i <= orders; i++) {
        if(i == 2) continue;   // skip one order
        printf("Order %d processed\n", i);
    }

    int battery = 2;
    while(battery > 0) {
        printf("Using phone\n");
        battery--;
    }

    int pin = 1234;
    do {
        printf("Enter PIN\n");
        pin--;
    } while(pin != 1234);

    return 0;
}
```

---

# ❌ COMMON MISTAKES (Interview Trap 😈)

❌ Infinite loop (condition update bhool gaye)
❌ Missing `break` in switch
❌ Using `=` instead of `==`
❌ Wrong loop selection

---

# 🏁 SUMMARY

✅ Control flow = program ka brain
✅ Loops = repetition power
✅ Correct loop = clean logic

---

## 🔥 Bro Tip

> **Agar loops clear hain, to logic building unstoppable hai** 🧠🚀

📌 Happy Coding – Control Your Code Flow 😎
