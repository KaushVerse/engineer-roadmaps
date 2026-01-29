# 📚 CommonActions – Deep Dive

> **CommonActions** React Navigation ka core utility hai jo navigation ko **action-based control** deta hai. Ye canvas advanced flows (auth, deep linking, global navigation) ke liye must-know hai.

---

## 🤔 CommonActions kya hai?

* `CommonActions` ek **helper object** hai
* Isme functions hote hain jo **navigation actions** return karte hain
* Ye actions `navigation.dispatch()` ke saath use hote hain

👉 Jab normal `navigation.navigate()` kaafi nahi hota, tab **CommonActions ka use hota hai**.

---

## 🎨 Import

```ts
import { CommonActions } from '@react-navigation/native';
```

---

## 📊 CommonActions – Methods (Deep Dive)

| 🧩 Method          | 🔍 Description                           | 🖼️ | Example                                                                |
| ------------------ | ---------------------------------------- | --- | ---------------------------------------------------------------------- |
| `navigate`         | Screen pe navigate karo (params ke sath) | 🧭  | `dispatch(CommonActions.navigate({ name:'Profile', params:{id:42} }))` |
| `goBack`           | Pichle screen pe jao                     | ↩️  | `dispatch(CommonActions.goBack())`                                     |
| `reset`            | Pura navigation state reset              | 🧹  | `reset({ index:0, routes:[{name:'Home'}] })`                           |
| `setParams`        | Current route params update              | ✍️  | `setParams({ userId:101 })`                                            |
| `getStateFromPath` | URL → navigation state                   | 🌐  | `getStateFromPath('/profile/42')`                                      |
| `getPathFromState` | Navigation state → URL                   | 🛤️ | `getPathFromState(state)`                                              |

---

## 🎯 Example Usage

### 1️⃣ Navigate using dispatch

```ts
navigation.dispatch(
  CommonActions.navigate({
    name: 'Profile',
    params: { userId: 42 },
  })
);
```

---

### 2️⃣ Reset Navigation State (Auth Flow)

```ts
navigation.dispatch(
  CommonActions.reset({
    index: 0,
    routes: [{ name: 'Home' }],
  })
);
```

---

### 3️⃣ Go Back

```ts
navigation.dispatch(CommonActions.goBack());
```

---

### 4️⃣ Update Params

```ts
navigation.dispatch(CommonActions.setParams({ filter: 'latest' }));
```

---

## ⚡ When to Use CommonActions?

| 🧠 Situation              | Reason                            |
| ------------------------- | --------------------------------- |
| Global navigation service | Screen ke bahar se navigate karna |
| Auth flows                | Login / Logout ke baad reset      |
| Nested navigators         | Unified action bhejna             |
| Deep linking              | URL ↔ state conversion            |

---

## 🏆 Best Practices (Industry Grade)

* ✅ Normal cases me `navigation.navigate()` use karo
* 🎯 `CommonActions.navigate` sirf **advanced / global** cases me
* 🔐 Auth flows ke liye **`reset` best choice**
* 🌐 Deep linking apps me `getStateFromPath` & `getPathFromState` mandatory
* 🧹 `setParams` tab use karo jab dispatch zaroori ho

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **navigate() = shortcut**
> **CommonActions + dispatch = full control**

---

## 🚀 Quick Recap

* 🧭 `navigate` → dispatch based navigation
* ↩️ `goBack` → previous screen
* 🧹 `reset` → new navigation tree
* ✍️ `setParams` → params update
* 🌐 `getStateFromPath` → URL → state
* 🛤️ `getPathFromState` → state → URL

---

> ✅ **Rule of Thumb:**
> Agar navigation ko **state machine** jaise control karna hai → **CommonActions** use karo.

Mastered 🔥🧠
