# 🚀 StackActions, DrawerActions & TabActions – Deep Dive (Hinglish)

> Ye canvas **React Navigation ke 3 power action objects** ko cover karta hai. Agar `dispatch()` engine hai, to ye uske **gear boxes** hain ⚙️

---

# 📚 StackActions

## 🤔 Kya hai?

`StackActions` stack navigator ke liye **low-level control** deta hai:

* Stack ke andar screens **add / replace / remove** kar sakte ho
* Mostly use hota hai → `navigation.dispatch(StackActions.xyz())`

---

## 🎨 Import

```ts
import { StackActions } from '@react-navigation/native';
```

---

## 📊 StackActions Methods

| 🧩 Method  | 🔍 Description                | 🖼️ | Example                                          |
| ---------- | ----------------------------- | --- | ------------------------------------------------ |
| `push`     | New screen top pe add         | ➕   | `dispatch(StackActions.push('Profile',{id:42}))` |
| `replace`  | Current screen replace        | 🔄  | `dispatch(StackActions.replace('Login'))`        |
| `pop`      | N screens remove              | 📤  | `dispatch(StackActions.pop(2))`                  |
| `popToTop` | Sirf root chhod ke sab remove | 🏔️ | `dispatch(StackActions.popToTop())`              |

---

## 🎯 StackActions Use Cases

* ➕ **push** → same screen multiple times (Profile → Profile)
* 🔄 **replace** → Login → Home (no back)
* 📤 **pop** → 2 screens peeche jana
* 🏔️ **popToTop** → Logout ke baad root

---

## 🏆 Best Practices (Stack)

* Simple back → `navigation.goBack()`
* Auth flows → `replace`
* Deep stacks → `popToTop`
* Overuse mat karo ❌

---

# 🚪 DrawerActions

## 🤔 Kya hai?

`DrawerActions` drawer navigator ko **programmatically control** karta hai:

* Open / Close / Toggle drawer
* Drawer ke andar **direct screen jump**

---

## 🎨 Import

```ts
import { DrawerActions } from '@react-navigation/native';
```

---

## 📊 DrawerActions Methods

| 🧩 Method      | 🔍 Description     | 🖼️ | Example                                      |
| -------------- | ------------------ | --- | -------------------------------------------- |
| `openDrawer`   | Drawer open        | 📂  | `dispatch(DrawerActions.openDrawer())`       |
| `closeDrawer`  | Drawer close       | 🚪  | `dispatch(DrawerActions.closeDrawer())`      |
| `toggleDrawer` | Open ↔ Close       | 🔀  | `dispatch(DrawerActions.toggleDrawer())`     |
| `jumpTo`       | Drawer screen jump | 🏷️ | `dispatch(DrawerActions.jumpTo('Settings'))` |

---

## 🎯 DrawerActions Use Cases

* 📂 Custom hamburger → `toggleDrawer`
* 🚪 Item select ke baad → `closeDrawer`
* 🏷️ Direct screen jump → `jumpTo`

---

## 🏆 Best Practices (Drawer)

* Hamburger icon → `toggleDrawer()`
* Direct switch → `jumpTo()`
* Auth/logout ke baad drawer close karo

---

# 🏷️ TabActions

## 🤔 Kya hai?

`TabActions` tab navigator ke liye **programmatic tab switching** deta hai.

* Mostly use hota hai → `jumpTo`

---

## 🎨 Import

```ts
import { TabActions } from '@react-navigation/native';
```

---

## 📊 TabActions Methods

| 🧩 Method  | 🔍 Description          | 🖼️ | Example                                    |
| ---------- | ----------------------- | --- | ------------------------------------------ |
| `jumpTo`   | Direct tab switch       | 🏷️ | `dispatch(TabActions.jumpTo('Feed'))`      |
| `navigate` | Tab navigate (shortcut) | 🧭  | `dispatch(TabActions.navigate('Profile'))` |

---

## 🎯 TabActions Use Cases

* 🏷️ Custom tab button
* 🧭 Programmatic tab switch
* 📦 Params ke sath tab open

---

## 🏆 Best Practices (Tabs)

* Direct tab switch → `jumpTo`
* Custom tab bar → `TabActions`
* Multiple dispatch avoid karo ❌

---

## 🧠 Mental Model (Interview Gold ✨)

* **StackActions** → Screen history control 📚
* **DrawerActions** → Side menu control 🚪
* **TabActions** → Section switcher 🏷️

---

## 🚀 Quick Recap

* ➕ `push` | 🔄 `replace` | 📤 `pop` | 🏔️ `popToTop`
* 📂 `openDrawer` | 🚪 `closeDrawer` | 🔀 `toggleDrawer` | 🏷️ `jumpTo`
* 🏷️ `jumpTo` (Tabs) | 🧭 `navigate`

---

> ✅ **Rule of Thumb:**
> Stack = history
> Drawer = menu
> Tabs = sections

Mastered 🚀🔥
