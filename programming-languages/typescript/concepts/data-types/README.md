# 🟦 TypeScript Basics – Core Types (with Code & Icons)

---

## 🟦 Type Annotation

**Meaning:** Variable, function, ya parameter ka type explicitly batana.

```ts
let age: number = 25;
let username: string = "Rahul";
```

👉 TS ko clearly pata hota hai kaunsa type expect karna hai.

---

## 🧩 Type Inference

**Meaning:** TS khud type guess kar leta hai value dekh kar.

```ts
let count = 10;      // number
let isAdmin = true; // boolean
```

👉 Explicit type likhne ki zarurat nahi.

---

## 🔤 Primitive Types

**Meaning:** Basic built‑in types.

```ts
let id: number = 1;
let name: string = "Amit";
let active: boolean = false;
```

👉 Simple values ke liye use hota hai.

---

## 📦 Object Types

**Meaning:** Object ke andar keys aur unke types define karna.

```ts
type User = {
  id: number;
  name: string;
};

const user: User = { id: 1, name: "Ravi" };
```

👉 Structure fixed rehta hai.

---

## 📚 Array Types

**Meaning:** Same type ke multiple values.

```ts
let scores: number[] = [10, 20, 30];
let names: Array<string> = ["A", "B"];
```

👉 List of values with same type.

---

## 🔁 Tuple

**Meaning:** Fixed length + fixed order array.

```ts
let userTuple: [number, string] = [1, "Raj"];
```

👉 Order aur type dono important.

---

## 🔢 Enum

**Meaning:** Named constants ka group.

```ts
enum Status {
  Pending,
  Success,
  Failed,
}

let current: Status = Status.Success;
```

👉 Readable aur safe values.

---

## ❓ Any

**Meaning:** Type checking off.

```ts
let data: any = 10;
data = "hello";
data = true;
```

⚠️ Avoid karo – type safety khatam.

---

## 🚫 Unknown

**Meaning:** Any jaisa hai but safe.

```ts
let value: unknown;
value = "text";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

👉 Use karne se pehle check zaruri.

---

## ⚫ Void

**Meaning:** Function kuch return nahi karta.

```ts
function logMessage(msg: string): void {
  console.log(msg);
}
```

👉 Mostly functions ke liye.

---

## 🧱 Never

**Meaning:** Function kabhi complete hi nahi hota.

```ts
function throwError(): never {
  throw new Error("Crash");
}
```

👉 Infinite loop / error case.

---

## 🧠 Boolean

**Meaning:** true / false.

```ts
let isLoggedIn: boolean = true;
```

---

## 🔠 String

**Meaning:** Text data.

```ts
let title: string = "TypeScript";
```

---

## 🔢 Number

**Meaning:** All numbers (int + float).

```ts
let price: number = 99.99;
```

---

## 📐 BigInt

**Meaning:** Bahut bade numbers.

```ts
let bigNumber: bigint = 12345678901234567890n;
```

⚠️ `n` lagana compulsory.

---

### ✅ Tip

> Ye saare basics strong ho gaye to **90% TypeScript errors khud solve ho jaate hain** 💪

Agar chaho next:

* 🧩 Advanced Types
* 🧠 Interview Q&A
* 🧪 Real‑world examples
* 📘 One‑page cheatsheet
