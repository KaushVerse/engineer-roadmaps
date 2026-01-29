# 🎧 Navigation Listeners – addListener / removeListener Deep Dive

> **React Navigation events system** ka complete, Hinglish + icon-based reference. Ye canvas **lifecycle understanding + real-world usage** dono ke liye perfect hai.

---

## 🤔 What is `addListener`?

`addListener` navigation ka **event subscription system** hai.

Isse tu screen ke lifecycle aur navigation events ko **listen (sun)** kar sakta hai:

* Screen focus / blur
* Back press / swipe back
* Transition start / end
* Navigation state changes

Har listener ke saath ek **callback** attach hota hai.

---

## 🤔 What is `removeListener`?

`removeListener` ka kaam hai **pehle se lage hue listener ko hataana**.

React Navigation me mostly tu directly `removeListener` use nahi karega, kyunki:

👉 `addListener` **ek unsubscribe function return karta hai**
👉 Usko call karna hi best cleanup method hai

---

## 📊 Common Navigation Events

| 🔔 Event          | 🔍 Description                   | 🖼️ | Real Use Case           |
| ----------------- | -------------------------------- | --- | ----------------------- |
| `focus`           | Screen visible ho jati hai       | 👀  | API call / refresh data |
| `blur`            | Screen chhod dete ho             | 🏃  | Timer stop, cleanup     |
| `beforeRemove`    | Screen remove hone wali hoti hai | ⏳   | Back confirm dialog     |
| `state`           | Navigation state change          | 🔄  | Debug / analytics       |
| `transitionStart` | Transition start                 | 🎬  | Animation / loader      |
| `transitionEnd`   | Transition end                   | ✅   | Final UI update         |

---

## ⚡ Usage Example (Hinglish Comments)

```tsx
import { useEffect } from 'react';
import { Text } from 'react-native';

function ProfileScreen({ navigation }) {
  useEffect(() => {
    // 👂 Focus listener
    const unsubscribeFocus = navigation.addListener('focus', () => {
      console.log('👀 Profile Screen focused');
    });

    // 👂 Blur listener
    const unsubscribeBlur = navigation.addListener('blur', () => {
      console.log('🏃 Profile Screen blurred');
    });

    // ⏳ Before remove (back intercept)
    const unsubscribeBeforeRemove = navigation.addListener(
      'beforeRemove',
      (e) => {
        e.preventDefault();
        alert('⚠️ Are you sure you want to leave?');
      }
    );

    // 🧹 Cleanup (remove listeners)
    return () => {
      unsubscribeFocus();
      unsubscribeBlur();
      unsubscribeBeforeRemove();
    };
  }, [navigation]);

  return <Text>👤 Profile Screen</Text>;
}
```

---

## 🧠 Deep Concepts (Interview + Debugging Gold)

| 🧩 Concept         | 🔍 Explanation                                   | 🖼️ |
| ------------------ | ------------------------------------------------ | --- |
| Subscription       | `addListener` ek unsubscribe fn return karta hai | 🎧  |
| Auto Cleanup       | useEffect return me unsubscribe → no memory leak | 🧹  |
| Multiple Listeners | Ek event pe multiple listeners ho sakte hain     | 🎶  |
| `beforeRemove`     | Back button / swipe intercept                    | 🚪  |
| Integration        | Analytics, logs, API triggers                    | 📊  |

---

## 📊 Summary Table

| 🧩 Function                 | 🔍 Purpose                 | 🖼️ | Example                                   |
| --------------------------- | -------------------------- | --- | ----------------------------------------- |
| `addListener(event, cb)`    | Event sunna                | 🎧  | `addListener('focus', cb)`                |
| `removeListener(event, cb)` | Manually listener hataana  | ❌   | `removeListener('focus', cb)`             |
| `unsubscribe()`             | Auto cleanup (recommended) | 🧹  | `const unsub = addListener(...); unsub()` |

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **Navigation = Event Emitter**
> **addListener = on()**
> **unsubscribe = off()**

---

> ✅ **Best Practice:**
>
> * Hamesha listeners ko `useEffect` ke andar add karo
> * Cleanup me **unsubscribe call karna mat bhoolna**
> * Heavy logic ke liye `useFocusEffect` bhi consider karo

Happy Listening 🎧🚀
