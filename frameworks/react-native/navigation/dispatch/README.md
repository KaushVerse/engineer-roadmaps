# 📚 dispatch() – Navigation Actions Deep Dive

> **dispatch()** React Navigation ka low-level power tool hai. Agar `navigate()` shortcut hai, to `dispatch()` **manual gearbox** hai 🔧 — full control.

---

## 🤔 dispatch() kya hai?

* `dispatch()` ek method hai jo **navigation action ko manually fire** karta hai
* Redux ke `dispatch(action)` jaisa behave karta hai
* `navigation.navigate()` internally bhi 👉 `dispatch(CommonActions.navigate())` hi call karta hai

👉 Matlab `dispatch()` = **advanced + explicit navigation control**

---

## 📊 Syntax

```ts
navigation.dispatch(action)
```

* `action` → `CommonActions / StackActions / DrawerActions / TabActions / custom`

---

## 📊 Dispatch Actions – Complete Table

| 🧩 Action Source            | 🔍 Description         | 🖼️ | Example                                              |
| --------------------------- | ---------------------- | --- | ---------------------------------------------------- |
| `CommonActions.navigate`    | Screen pe navigate     | 🧭  | `dispatch(CommonActions.navigate({name:'Profile'}))` |
| `CommonActions.goBack`      | Pichle screen pe       | ↩️  | `dispatch(CommonActions.goBack())`                   |
| `CommonActions.reset`       | Navigation tree reset  | 🧹  | `reset({index:0,routes:[{name:'Home'}]})`            |
| `CommonActions.setParams`   | Params update          | ✍️  | `setParams({sort:'latest'})`                         |
| `StackActions.push`         | Stack me naya screen   | ➕   | `push('Profile',{id:2})`                             |
| `StackActions.replace`      | Current screen replace | 🔄  | `replace('Home')`                                    |
| `StackActions.pop`          | N screens pop          | 📤  | `pop(2)`                                             |
| `StackActions.popToTop`     | Root screen            | 🏔️ | `popToTop()`                                         |
| `DrawerActions.openDrawer`  | Drawer open            | 📂  | `openDrawer()`                                       |
| `DrawerActions.closeDrawer` | Drawer close           | 🚪  | `closeDrawer()`                                      |
| `TabActions.jumpTo`         | Tab jump               | 🏷️ | `jumpTo('Settings')`                                 |

---

## 🎨 Example Usages

### 1️⃣ Navigate using dispatch

```ts
import { CommonActions } from '@react-navigation/native';

navigation.dispatch(
  CommonActions.navigate({
    name: 'Profile',
    params: { userId: 42 },
  })
);
```

---

### 2️⃣ Stack Replace (Auth Flow)

```ts
import { StackActions } from '@react-navigation/native';

navigation.dispatch(StackActions.replace('Login'));
```

---

### 3️⃣ Drawer Open

```ts
import { DrawerActions } from '@react-navigation/native';

navigation.dispatch(DrawerActions.openDrawer());
```

---

### 4️⃣ Tab JumpTo

```ts
import { TabActions } from '@react-navigation/native';

navigation.dispatch(TabActions.jumpTo('Feed'));
```

---

## ⚡ Why Use dispatch()?

| Situation                 | Why dispatch is better                      |
| ------------------------- | ------------------------------------------- |
| Global navigation service | navigation prop available nahi hota         |
| Auth login/logout         | Pure tree reset chahiye                     |
| Nested navigators         | Exact navigator ko target karna             |
| Custom flows              | Navigation ko state-machine jaisa use karna |

---

## 🏆 Best Practices

* ✅ Normal cases → `navigation.navigate()`
* ⚡ Advanced / global cases → `dispatch()`
* 🧠 Hamesha **correct action creator** use karo
* 🔐 Auth / onboarding → `reset + dispatch` combo

---

## 🧠 Mental Model (Yaad Rakhne Ka Rule)

> **navigate() = shortcut**
> **dispatch(action) = full control**

---

## 🚀 Quick Recap

* 🧭 navigate → via dispatch
* ↩️ goBack → previous
* 🧹 reset → fresh tree
* ✍️ setParams → update params
* ➕ push | 🔄 replace | 📤 pop | 🏔️ popToTop
* 📂 openDrawer | 🚪 closeDrawer
* 🏷️ jumpTo (tabs)

---

> ✅ **Rule of Thumb:**
> Jab navigation ko **Redux jaisa control** chahiye → `dispatch()` use karo.

Mastered 🚀🔥
