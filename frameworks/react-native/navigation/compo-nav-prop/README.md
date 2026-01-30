# 🧩 CompositeNavigationProp – Deep Dive (Hinglish)

> **CompositeNavigationProp** React Navigation ka advanced **TypeScript utility type** hai jo **multiple navigators ke navigation types ko combine** karta hai. Ye nested navigators (Stack + Tabs / Stack + Drawer) ke liye *game changer* hai 🔥

---

## 🤔 CompositeNavigationProp kya hai?

`CompositeNavigationProp<A, B>` ka simple matlab:

> “Mera screen **A navigator** ke andar bhi hai aur **B navigator** ke andar bhi — dono ke navigation methods mujhe ek hi object me type-safe chahiye.”

Isse tu ek hi `navigation` object se:

* Stack routes
* Tab routes
* Drawer routes

dono ko safely access kar sakta hai.

---

## 🎨 Import

```ts
import { CompositeNavigationProp } from '@react-navigation/native';
import { StackNavigationProp } from '@react-navigation/stack';
import { BottomTabNavigationProp } from '@react-navigation/bottom-tabs';
```

---

## 📊 Syntax

```ts
CompositeNavigationProp<PrimaryNav, SecondaryNav>
```

---

## 🧩 Generic Parameters Explained

| 🧩 Generic     | 🔍 Description           | 🖼️ | Example                                         |
| -------------- | ------------------------ | --- | ----------------------------------------------- |
| `PrimaryNav`   | Main navigator ka type   | 📑  | `StackNavigationProp<StackParamList,'Profile'>` |
| `SecondaryNav` | Nested navigator ka type | 🏷️ | `BottomTabNavigationProp<TabParamList>`         |

---

## 🎯 Example – Stack Inside Tabs (Most Common)

```tsx
type StackParamList = {
  Home: undefined;
  Profile: { userId: number };
};

type TabParamList = {
  Feed: undefined;
  Settings: undefined;
};

// 🔗 Composite Navigation Type
type ProfileScreenNavProp = CompositeNavigationProp<
  StackNavigationProp<StackParamList, 'Profile'>,
  BottomTabNavigationProp<TabParamList>
>;

// 🧩 Props
type Props = { navigation: ProfileScreenNavProp };

function ProfileScreen({ navigation }: Props) {
  return (
    <>
      <Button
        title="Go Home (Stack)"
        onPress={() => navigation.navigate('Home')}
      />
      <Button
        title="Go Settings (Tab)"
        onPress={() => navigation.navigate('Settings')}
      />
    </>
  );
}
```

✅ Ab `navigation.navigate()` **Stack + Tab dono ke routes** ko type-safe samajhta hai.

---

## 📊 Available Methods (Combined Power)

| 🧩 Method   | 🔍 Description       | 🖼️ | Example                           |
| ----------- | -------------------- | --- | --------------------------------- |
| `navigate`  | Stack / Tab screen   | 🧭  | `navigate('Profile',{userId:42})` |
| `push`      | Stack me naya screen | ➕   | `push('Profile',{userId:1})`      |
| `replace`   | Current replace      | 🔄  | `replace('Home')`                 |
| `goBack`    | Back                 | ↩️  | `goBack()`                        |
| `pop`       | N screens pop        | 📤  | `pop(2)`                          |
| `popToTop`  | Stack root           | 🏔️ | `popToTop()`                      |
| `jumpTo`    | Tab jump             | 🏷️ | `jumpTo('Settings')`              |
| `setParams` | Params update        | ✍️  | `setParams({filter:'latest'})`    |

---

## ⚡ When to Use CompositeNavigationProp?

| Situation           | Reason                                |
| ------------------- | ------------------------------------- |
| Stack inside Tabs   | Dono ke routes access chahiye         |
| Stack inside Drawer | Drawer + stack methods ek jagah       |
| Nested navigation   | TypeScript errors avoid karne ke liye |

❌ Single navigator ho → Composite ki zarurat nahi.

---

## 🏆 Best Practices (Industry Grade)

* ✅ Har navigator ke liye **alag ParamList**
* ✅ Sirf **nested screens** me Composite use karo
* 🎯 Order matter karta hai → pehle *primary* navigator
* ⚡ Screen props me type assign karo (hooks ke liye bhi)
* 🧹 Large apps → param lists alag files me rakho

---

## 🧠 Mental Model (Yaad Rakhne Ka Rule)

> **Single navigator** → Simple NavigationProp
> **Nested navigator** → CompositeNavigationProp 🔗

---

## 🚀 Quick Recap

* 📑 PrimaryNav → Main navigator
* 🏷️ SecondaryNav → Nested navigator
* 🧭 navigate → Stack + Tab safe
* ➕ push → Stack
* 🏷️ jumpTo → Tabs
* 🔄 replace / 📤 pop / 🏔️ popToTop

---

> ✅ **Rule of Thumb:**
> Agar ek screen se **multiple navigator routes** hit ho rahe hain → **CompositeNavigationProp** mandatory.

Mastered 🧠🔥
