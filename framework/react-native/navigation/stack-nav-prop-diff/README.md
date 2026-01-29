# 📚 StackNavigationProp vs StackNavigationProps (Deep Dive)

> React Navigation + TypeScript me ye **most confusing but most important** difference hai. Is canvas ke baad doubt zero ho jayega 🔥

---

## 🧩 High‑Level Difference

| 🧩 Type                  | 🔍 Description                                                           | 🖼️ | Example                                                    |
| ------------------------ | ------------------------------------------------------------------------ | --- | ---------------------------------------------------------- |
| **StackNavigationProp**  | Sirf `navigation` object ko type‑safe banata hai                         | 🎯  | `{ navigation: StackNavigationProp<ParamList,'Profile'> }` |
| **StackNavigationProps** | `navigation + route` dono ko ek saath type karta hai (full screen props) | ⚡   | `type Props = StackNavigationProps<ParamList,'Profile'>`   |

---

## 📊 Syntax Comparison

### 🔹 StackNavigationProp (Single)

```ts
type StackNavigationProp<ParamList, RouteName?>;
```

### 🔹 StackNavigationProps (Combined – Conceptual)

```ts
type StackNavigationProps<ParamList, RouteName?> = {
  navigation: StackNavigationProp<ParamList, RouteName>;
  route: RouteProp<ParamList, RouteName>;
};
```

👉 Note: Real library me **ye role `StackScreenProps` play karta hai**.

---

## 🎨 Practical Example (Navigation + Route)

```tsx
import { StackNavigationProp } from '@react-navigation/stack';
import { RouteProp } from '@react-navigation/native';

// 1️⃣ Param list
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: number };
};

// 2️⃣ Screen props type
type ProfileScreenProps = {
  navigation: StackNavigationProp<RootStackParamList, 'Profile'>;
  route: RouteProp<RootStackParamList, 'Profile'>;
};

// 3️⃣ Use in component
function ProfileScreen({ navigation, route }: ProfileScreenProps) {
  return (
    <Button
      title="Go Home"
      onPress={() => navigation.navigate('Home')}
    />
  );
}
```

---

## 🚀 Short & Recommended Way (Industry Standard)

```tsx
import { StackScreenProps } from '@react-navigation/stack';

type ProfileProps = StackScreenProps<RootStackParamList, 'Profile'>;

function ProfileScreen({ navigation, route }: ProfileProps) {
  // navigation + route both typed
}
```

✅ This replaces **StackNavigationProps** idea completely.

---

## 📊 Deep Dive: What You Actually Get

| 🧩 Property    | 🔍 Description              | 🖼️ | Example                       |
| -------------- | --------------------------- | --- | ----------------------------- |
| `navigation`   | Stack navigation controller | 🧭  | `navigation.navigate('Home')` |
| `route`        | Current route info          | 🗺️ | `route.params.userId`         |
| `route.key`    | Unique route key            | 🔑  | `Profile-xyz123`              |
| `route.name`   | Screen name                 | 🏷️ | `Profile`                     |
| `route.params` | Typed params                | 📦  | `{ userId: 42 }`              |

---

## 🏆 Best Practices (Golden Rules)

* 🎯 **Only navigation chahiye** → `StackNavigationProp`
* ⚡ **Navigation + params chahiye** → `StackScreenProps`
* 📑 Har navigator ke liye **alag ParamList**
* 🧠 Screen components me **StackScreenProps prefer karo**
* 🔁 Reusable components me `useNavigation<StackNavigationProp<...>>()`

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **StackNavigationProp** → Controller 🎮
> **RouteProp** → Data 📦
> **StackScreenProps** → Controller + Data ⚡

---

## 🚀 Quick Recap

* 🎯 `StackNavigationProp` → sirf navigation
* ⚡ `StackNavigationProps` → conceptually navigation + route
* ✅ Real‑world me **StackScreenProps** use hota hai
* 🧭 Methods: navigate, push, replace, goBack, pop, reset
* 🗺️ Route: key, name, params, path

---

> ✅ **Rule of Thumb:**
> Screen likh rahe ho? → **StackScreenProps**
> Button / helper component? → **StackNavigationProp**

Mastered 🧠🔥
