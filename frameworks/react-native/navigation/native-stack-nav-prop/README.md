# 📚 NativeStackNavigationProp – Deep Dive (TypeScript)

> **NativeStackNavigationProp** React Navigation ka ek **TypeScript utility type** hai jo **Native Stack Navigator** (`@react-navigation/native-stack`) ke navigation methods ko **100% type-safe** bana deta hai.

---

## 🤔 NativeStackNavigationProp kya hai?

* Ye **generic TypeScript type** hai
* Sirf **Native Stack Navigator** ke liye hota hai
* `react-native-screens` par based hota hai (better performance)
* Galat route ya params → **compile-time error** ✅

---

## 📊 Syntax

```ts
type NativeStackNavigationProp<ParamList, RouteName?>
```

---

## 🧩 Generic Parameters Explained

| 🧩 Generic   | 🔍 Description               | 🖼️ | Example                                        |
| ------------ | ---------------------------- | --- | ---------------------------------------------- |
| `ParamList`  | Navigator ke routes + params | 📑  | `{ Home: undefined; Profile:{userId:number} }` |
| `RouteName?` | Specific screen ka naam      | 🏷️ | `'Profile'`                                    |

---

## 🎨 Basic Example (TypeScript)

```tsx
import { NativeStackNavigationProp } from '@react-navigation/native-stack';

// 1️⃣ Param list
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: number };
  Settings: { mode: string } | undefined;
};

// 2️⃣ Navigation type for Profile screen
type ProfileNavProp = NativeStackNavigationProp<
  RootStackParamList,
  'Profile'
>;

// 3️⃣ Use in props
type Props = { navigation: ProfileNavProp };

function ProfileScreen({ navigation }: Props) {
  return (
    <Button
      title="Go Settings"
      onPress={() => navigation.navigate('Settings', { mode: 'dark' })}
    />
  );
}
```

---

## 📊 NativeStackNavigationProp – Methods

| 🧩 Method   | 🔍 Description          | 🖼️ | Example                                   |
| ----------- | ----------------------- | --- | ----------------------------------------- |
| `navigate`  | Screen pe jao + params  | 🧭  | `navigate('Profile',{userId:42})`         |
| `push`      | Naya instance push      | ➕   | `push('Profile',{userId:42})`             |
| `replace`   | Current screen replace  | 🔄  | `replace('Home')`                         |
| `goBack`    | Pichle screen pe        | ↩️  | `goBack()`                                |
| `pop`       | Multiple screens remove | 📤  | `pop(2)`                                  |
| `popToTop`  | Root screen             | 🏔️ | `popToTop()`                              |
| `setParams` | Params update           | ✍️  | `setParams({userId:100})`                 |
| `reset`     | Stack reset             | 🧹  | `reset({index:0,routes:[{name:'Home'}]})` |
| `canGoBack` | Back possible hai?      | 🔙  | `if(canGoBack()) goBack()`                |
| `getParent` | Parent navigator        | 👥  | `getParent()?.navigate('Root')`           |
| `getId`     | Navigator ID            | 🆔  | `navigation.getId()`                      |

---

## ⚡ Usage Patterns

### 1️⃣ Screen Props me

```tsx
function HomeScreen({
  navigation,
}: {
  navigation: NativeStackNavigationProp<RootStackParamList, 'Home'>;
}) {
  return (
    <Button
      title="Go Profile"
      onPress={() => navigation.navigate('Profile', { userId: 1 })}
    />
  );
}
```

---

### 2️⃣ Hook ke saath (Reusable Components)

```tsx
import { useNavigation } from '@react-navigation/native';

const navigation = useNavigation<
  NativeStackNavigationProp<RootStackParamList>
>();
```

---

## 🏆 Best Practices (Industry Grade)

* ✅ Har **Native Stack** ke liye ek `ParamList`
* 🎯 Sirf navigation chahiye → `NativeStackNavigationProp`
* ⚡ Navigation + route dono chahiye → `NativeStackScreenProps`
* 🧠 Optional params ko `?` ya `| undefined` se define karo
* 🧹 Large apps me param lists **separate files** me rakho

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **ParamList = Navigation contract**
> **NativeStackNavigationProp = Native-stack ka typed controller**

---

## 🚀 Quick Recap

* 📑 ParamList → Routes + params
* 🏷️ RouteName → Specific screen
* 🧭 `navigate`
* ➕ `push`
* 🔄 `replace`
* ↩️ `goBack`
* 📤 `pop`
* 🏔️ `popToTop`
* ✍️ `setParams`
* 🧹 `reset`
* 👥 `getParent`
* 🆔 `getId`

---

> ✅ **Rule of Thumb:**
> Agar `createNativeStackNavigator` use kar rahe ho → **NativeStackNavigationProp** hi sahi choice hai.

Fast & Safe Navigation 🚀📱
