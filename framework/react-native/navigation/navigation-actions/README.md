# 📊 Navigation Actions – Deep Dive Cheat Sheet

> **React Navigation Actions** ka complete, visual + Hinglish reference. Ye file direct **GitHub README / Notion / Team Docs** ke liye ready hai.

---

## 🧠 Big Picture

React Navigation me **navigation methods internally action objects dispatch karti hain**.

4 main action groups hote hain:

* 🌍 **CommonActions** → sab navigators ke liye
* 📚 **StackActions** → Stack Navigator only
* 📂 **DrawerActions** → Drawer Navigator only
* 🏷️ **TabActions** → Bottom / Top Tabs only

---

## 🌍 CommonActions (Universal)

| 🧩 Action   | 🔍 Description                 | 🖼️ | Example                                       |
| ----------- | ------------------------------ | --- | --------------------------------------------- |
| `navigate`  | Screen pe navigate karo        | 🧭  | `dispatch(CommonActions.navigate('Profile'))` |
| `goBack`    | Ek step back jao               | ↩️  | `dispatch(CommonActions.goBack())`            |
| `reset`     | Pura navigation state reset    | 🧹  | `reset({ index:0, routes:[{name:'Home'}] })`  |
| `setParams` | Current route ke params update | ✍️  | `setParams({ id:42 })`                        |

---

## 📚 StackActions (Stack Navigator Only)

| 🧩 Action  | 🔍 Description                | 🖼️ | Example                  |
| ---------- | ----------------------------- | --- | ------------------------ |
| `push`     | Naya screen stack me add      | ➕   | `push('Profile',{id:1})` |
| `replace`  | Current screen replace        | 🔄  | `replace('Login')`       |
| `pop`      | Ek ya multiple screens remove | 📤  | `pop(2)`                 |
| `popToTop` | Seedha root screen            | 🏔️ | `popToTop()`             |

---

## 📂 DrawerActions (Drawer Navigator Only)

| 🧩 Action      | 🔍 Description      | 🖼️ | Example             |
| -------------- | ------------------- | --- | ------------------- |
| `openDrawer`   | Drawer open         | 📖  | `openDrawer()`      |
| `closeDrawer`  | Drawer close        | ❌   | `closeDrawer()`     |
| `toggleDrawer` | Open / close toggle | 🔄  | `toggleDrawer()`    |
| `jumpTo`       | Drawer item pe jump | 🏃  | `jumpTo('Profile')` |

---

## 🏷️ TabActions (Tab Navigator Only)

| 🧩 Action | 🔍 Description       | 🖼️ | Example              |
| --------- | -------------------- | --- | -------------------- |
| `jumpTo`  | Specific tab pe jump | 🏷️ | `jumpTo('Settings')` |

---

## ⚡ Example Code (Hinglish Comments)

```ts
import {
  CommonActions,
  StackActions,
  DrawerActions,
  TabActions,
} from '@react-navigation/native';

// 🌍 CommonActions
navigation.dispatch(
  CommonActions.reset({
    index: 0,
    routes: [{ name: 'Home' }],
  })
);

// 📚 StackActions
navigation.dispatch(StackActions.push('Profile', { userId: 42 }));
navigation.dispatch(StackActions.replace('Login'));
navigation.dispatch(StackActions.popToTop());

// 📂 DrawerActions
navigation.dispatch(DrawerActions.openDrawer());
navigation.dispatch(DrawerActions.toggleDrawer());

// 🏷️ TabActions
navigation.dispatch(TabActions.jumpTo('Explore'));
```

---

## 📊 Quick Recap Table

| 📦 Category      | 🧩 Actions                                    | 🖼️ |
| ---------------- | --------------------------------------------- | --- |
| 🌍 CommonActions | navigate, goBack, reset, setParams            | 🌍  |
| 📚 StackActions  | push, replace, pop, popToTop                  | 📚  |
| 📂 DrawerActions | openDrawer, closeDrawer, toggleDrawer, jumpTo | 📂  |
| 🏷️ TabActions   | jumpTo                                        | 🏷️ |

---

## 🧠 Mental Model (Interview Gold ✨)

* `navigate()` → **smart jump** (existing screen reuse)
* `push()` → **force new screen**
* `replace()` → **history remove**
* `reset()` → **clean slate** (auth flows)

---

> ✅ **Best Practice:**
>
> * Normally `navigation.navigate()` kaafi hota hai
> * `dispatch + Actions` tab use karo jab **complex flows / auth reset / deep control** chahiye

Happy Navigating 🚀📱
