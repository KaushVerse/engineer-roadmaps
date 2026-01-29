# 📚 StackNavigationProp – Deep Dive (TypeScript)

> **StackNavigationProp** React Navigation ka ek powerful **TypeScript utility type** hai jo `navigation` object ke methods ko **fully type-safe** bana deta hai.

---

## 🤔 StackNavigationProp kya hai?

* Ye ek **generic TypeScript type** hai
* `navigation.navigate / push / replace / goBack` jaise methods ko type-safe karta hai
* Galat **route name** ya **wrong params** → compile time error ✅

👉 Matlab runtime bugs se pehle hi TypeScript pakad leta hai.

---

## 📊 Syntax

```ts
type StackNavigationProp<ParamList, RouteName?>
```

---

## 🧩 Generic Parameters Explained

| 🧩 Generic   | 🔍 Meaning                         | 🖼️ | Example                                        |
| ------------ | ---------------------------------- | --- | ---------------------------------------------- |
| `ParamList`  | Stack ke saare routes + params     | 📑  | `{ Home: undefined; Profile:{userId:number} }` |
| `RouteName?` | Specific screen ka naam (optional) | 🏷️ | `'Profile'`                                    |

---

## 🎨 Basic Example (TypeScript)

```tsx
import { StackNavigationProp } from '@react-navigation/stack';

// 1️⃣ Define ParamList
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: number };
};

// 2️⃣ Navigation type for Profile screen
type ProfileNavProp = StackNavigationProp<
  RootStackParamList,
  'Profile'
>;

// 3️⃣ Use in props
type Props = {
  navigation: ProfileNavProp;
};

function ProfileScreen({ navigation }: Props) {
  return (
    <Button
      title="Go Home"
      onPress={() => navigation.navigate('Home')} // ✅ type safe
    />
  );
}
```

---

## 📊 StackNavigationProp – Methods

| 🧩 Method   | 🔍 Description         | 🖼️ | Example                                   |
| ----------- | ---------------------- | --- | ----------------------------------------- |
| `navigate`  | Screen pe jao + params | 🧭  | `navigate('Profile',{userId:42})`         |
| `push`      | Naya screen stack me   | ➕   | `push('Profile',{userId:42})`             |
| `replace`   | Current screen replace | 🔄  | `replace('Home')`                         |
| `goBack`    | Pichla screen          | ↩️  | `goBack()`                                |
| `pop`       | Multiple screens pop   | 📤  | `pop(2)`                                  |
| `popToTop`  | Root screen            | 🏔️ | `popToTop()`                              |
| `setParams` | Current params update  | ✍️  | `setParams({userId:99})`                  |
| `reset`     | Stack reset            | 🧹  | `reset({index:0,routes:[{name:'Home'}]})` |

---

## ⚡ Usage Patterns

### 1️⃣ Screen Props me

```tsx
function HomeScreen({
  navigation,
}: {
  navigation: StackNavigationProp<RootStackParamList, 'Home'>;
}) {
  return (
    <Button
      title="Profile"
      onPress={() => navigation.navigate('Profile', { userId: 1 })}
    />
  );
}
```

---

### 2️⃣ Custom Hook ke through (Clean Way)

```tsx
import { useNavigation } from '@react-navigation/native';

const navigation = useNavigation<
  StackNavigationProp<RootStackParamList>
>();
```

👉 Ye approach reusable components ke liye best hai.

---

## 🏆 Best Practices (Industry Grade)

* ✅ Har **Stack Navigator** ke liye ek `ParamList`
* ✅ Screen props me **StackNavigationProp** use karo
* 🎯 Route-specific ho → `<ParamList,'ScreenName'>`
* ⚡ Reusable components → `useNavigation<StackNavigationProp<...>>()`
* 🧹 Large apps → ParamLists ko **separate files** me rakho

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **ParamList = Navigation contract**
> **StackNavigationProp = Typed controller for that contract**

---

## 🚀 Quick Recap

* 📑 **ParamList** → All routes + params
* 🏷️ **RouteName** → Specific screen
* 🧭 `navigate`
* ➕ `push`
* 🔄 `replace`
* ↩️ `goBack`
* 📤 `pop`
* 🏔️ `popToTop`
* ✍️ `setParams`
* 🧹 `reset`

---

> ✅ **Rule of Thumb:**
> TypeScript + React Navigation = **RouteProp + StackNavigationProp** together.

Happy Navigating 🧭🚀
