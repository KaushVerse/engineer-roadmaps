# 📚 RouteProp – Deep Dive (TypeScript)

> **RouteProp** React Navigation ka ek powerful **TypeScript helper** hai jo screens ke params ko **100% type-safe** banata hai. Ye canvas real-world apps + interviews dono ke liye perfect hai.

---

## 🤔 RouteProp kya hai?

`RouteProp` ek **generic type** hai jo:

* Screen ke `route.params` ko strongly type karta hai
* Runtime bugs ko compile-time errors me convert karta hai
* TypeScript users ke liye **must-use** hai

---

## 📊 RouteProp Syntax

```ts
type RouteProp<ParamList, RouteName>
```

---

## 🧩 Generic Parameters Explained

| 🧩 Generic  | 🔍 Meaning                         | 🖼️ | Example                                    |
| ----------- | ---------------------------------- | --- | ------------------------------------------ |
| `ParamList` | Navigator ke saare routes + params | 📑  | `{ Home: undefined; Profile:{id:number} }` |
| `RouteName` | Specific screen ka key             | 🏷️ | `'Profile'`                                |

---

## 🎨 Basic Example (TypeScript)

```tsx
import { RouteProp } from '@react-navigation/native';

// 1️⃣ Define param list
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: number; username: string };
};

// 2️⃣ Create RouteProp for Profile
type ProfileRouteProp = RouteProp<RootStackParamList, 'Profile'>;

// 3️⃣ Use in screen
function ProfileScreen({ route }: { route: ProfileRouteProp }) {
  return (
    <Text>
      👤 UserID: {route.params.userId}, Name: {route.params.username}
    </Text>
  );
}
```

---

## 📊 RouteProp Properties

| 🧩 Property | 🔍 Description            | 🖼️ | Example          |
| ----------- | ------------------------- | --- | ---------------- |
| `key`       | Unique route identifier   | 🔑  | `Profile-abc123` |
| `name`      | Route name                | 🏷️ | `'Profile'`      |
| `params`    | Typed params object       | 📦  | `{ userId: 42 }` |
| `path?`     | Deep link path (optional) | 🌐  | `/profile/42`    |

---

## ⚡ Usage Patterns

| 🧩 Pattern        | 🔍 Description                    | 🖼️ | Example                         |
| ----------------- | --------------------------------- | --- | ------------------------------- |
| Stack Navigator   | Stack screens ke params type-safe | 📚  | `Stack.Screen name="Profile"`   |
| Tab Navigator     | Tabs me params typing             | 🏷️ | `Tab.Screen name="Feed"`        |
| Drawer Navigator  | Drawer screen params              | 📂  | `Drawer.Screen name="Settings"` |
| Nested Navigators | Root + nested param safety        | 🏗️ | `RouteProp<Root,'Nested'>`      |

---

## 🏆 Best Practices (Industry Grade)

* ✅ Har **Navigator** ke liye ek `ParamList` type banao
* ✅ Screen props ko **RouteProp se strictly type** karo
* 🎯 Optional params ko `?` se define karo
* ⚡ Nested navigators ke liye **alag param lists** rakho
* 🧹 Large apps me **union / composite param lists** use karo

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **ParamList = Navigation contract**
> **RouteProp = Screen ka typed view of that contract**

---

## 🚀 Quick Recap

* 📑 **ParamList** → Routes + params define karta hai
* 🏷️ **RouteName** → Specific screen key
* 🔑 **key** → Unique route instance
* 📦 **params** → Fully typed data
* 🌐 **path** → Deep linking support

---

> ✅ **Rule of Thumb:** Agar TypeScript use kar rahe ho aur RouteProp nahi use kar rahe → you’re missing safety.

Happy Typing 🧠⚡
