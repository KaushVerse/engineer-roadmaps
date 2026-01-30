# 🏷️ BottomTabNavigationProp – Deep Dive (TypeScript)

> **BottomTabNavigationProp** React Navigation ka TypeScript utility type hai jo **Bottom Tab Navigator** ke `navigation` object ko **fully type-safe** banata hai. Ye tabs ke andar screens ke liye must-know concept hai.

---

## 🤔 BottomTabNavigationProp kya hai?

* Ye ek **generic TypeScript type** hai
* Sirf **Bottom Tab Navigator** (`createBottomTabNavigator`) ke liye hota hai
* Tab navigation methods ko **compile-time safe** bana deta hai

👉 Galat tab name ya galat params pass karoge → TypeScript turant error dega ✅

---

## 🎨 Import

```ts
import { BottomTabNavigationProp } from '@react-navigation/bottom-tabs';
```

---

## 📊 Syntax

```ts
type BottomTabNavigationProp<ParamList, RouteName?>
```

---

## 🧩 Generic Parameters Explained

| 🧩 Generic   | 🔍 Description                   | 🖼️ | Example                                        |
| ------------ | -------------------------------- | --- | ---------------------------------------------- |
| `ParamList`  | Tab navigator ke routes + params | 📑  | `{ Home: undefined; Profile:{userId:number} }` |
| `RouteName?` | Specific tab screen ka naam      | 🏷️ | `'Profile'`                                    |

---

## 🎯 Basic Example (TypeScript)

```tsx
type TabParamList = {
  Home: undefined;
  Profile: { userId: number };
  Settings: { mode: string } | undefined;
};

// Profile tab ke liye navigation type
type ProfileNavProp = BottomTabNavigationProp<
  TabParamList,
  'Profile'
>;

type Props = { navigation: ProfileNavProp };

function ProfileScreen({ navigation }: Props) {
  return (
    <>
      <Button
        title="Go Home"
        onPress={() => navigation.navigate('Home')}
      />
      <Button
        title="Go Settings"
        onPress={() => navigation.navigate('Settings', { mode: 'dark' })}
      />
    </>
  );
}
```

---

## 📊 BottomTabNavigationProp – Methods

| 🧩 Method   | 🔍 Description            | 🖼️ | Example                           |
| ----------- | ------------------------- | --- | --------------------------------- |
| `navigate`  | Tab screen pe navigate    | 🧭  | `navigate('Profile',{userId:42})` |
| `jumpTo`    | Direct tab switch         | 🏷️ | `jumpTo('Settings')`              |
| `goBack`    | Previous screen           | ↩️  | `goBack()`                        |
| `setParams` | Current tab params update | ✍️  | `setParams({filter:'latest'})`    |
| `canGoBack` | Back possible?            | 🔙  | `if(canGoBack()) goBack()`        |
| `getParent` | Parent navigator          | 👥  | `getParent()?.navigate('Root')`   |
| `getState`  | Tab navigator state       | 🗺️ | `getState()`                      |

---

## ⚡ When to Use BottomTabNavigationProp?

| Situation               | Why                                     |
| ----------------------- | --------------------------------------- |
| Tab screen likh rahe ho | Correct navigation typing               |
| TypeScript strict mode  | Route safety chahiye                    |
| Nested navigation       | CompositeNavigationProp ke sath combine |

❌ Stack-only screen ho → StackNavigationProp better.

---

## 🏆 Best Practices (Industry Grade)

* ✅ Har **Tab Navigator** ke liye ek `ParamList`
* 🎯 Screen-specific ho → `<ParamList,'ScreenName'>`
* ⚡ Nested navigators → `CompositeNavigationProp`
* 🧠 Optional params ko `?` ya `| undefined` se define karo
* 🧹 ParamLists ko **separate files** me rakho

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **BottomTabNavigationProp = Tabs ka typed controller** 🏷️

---

## 🚀 Quick Recap

* 📑 ParamList → Tab routes + params
* 🏷️ RouteName → Specific tab
* 🧭 `navigate`
* 🏷️ `jumpTo`
* ↩️ `goBack`
* ✍️ `setParams`
* 🔙 `canGoBack`
* 👥 `getParent`
* 🗺️ `getState`

---

> ✅ **Rule of Thumb:**
> Agar screen **Bottom Tabs ke andar** hai → **BottomTabNavigationProp** use karo.

Tabbed & Typed 🚀🔥
