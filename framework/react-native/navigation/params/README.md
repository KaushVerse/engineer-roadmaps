# 📊 Navigation Params – Deep Dive Cheat Sheet

> **React Navigation Params** ka complete, visual + Hinglish reference. Ye file direct **GitHub README / Notion / Docs** ke liye ready hai.

---

## 🔑 Basic Concept

**Params = data jo ek screen se dusri screen ko bheja jata hai.**

Params 3 jagah handle hote hain:

1️⃣ **Sending Params** → `navigate / push / replace`
2️⃣ **Receiving Params** → `route.params`
3️⃣ **Updating Params** → `navigation.setParams`

---

## 🏗️ Sending Params

| 🔧 Method                | 🔍 Description                        | 🖼️ | Example                                |
| ------------------------ | ------------------------------------- | --- | -------------------------------------- |
| `navigate(name, params)` | Screen pe jao + data bhejo            | 🧭  | `navigate('Profile', { userId: 42 })`  |
| `push(name, params)`     | Same screen ka naya instance stack me | ➕   | `push('Profile', { userId: 42 })`      |
| `replace(name, params)`  | Current screen replace karke bhejo    | 🔄  | `replace('Profile', { from: 'Home' })` |

---

## 📥 Receiving Params

| 🔑 Access         | 🔍 Description                     | 🖼️ | Example                           |
| ----------------- | ---------------------------------- | --- | --------------------------------- |
| `route.params`    | Screen ke andar params access      | 📦  | `const { userId } = route.params` |
| Optional chaining | Safe access (null crash se bachao) | ❓   | `route.params?.userId`            |
| Default value     | Param missing ho to fallback       | 🎯  | `route.params?.userId ?? 0`       |

---

## 🔄 Updating Params

| 🔧 Method   | 🔍 Description                   | 🖼️ | Example                     |
| ----------- | -------------------------------- | --- | --------------------------- |
| `setParams` | Existing screen ke params update | ✍️  | `setParams({ userId: 99 })` |
| Re-render   | Params update → auto re-render   | 🔁  | Auto                        |
| Use cases   | Filters, header title, tabs      | 🏷️ | Dynamic title               |

---

## 🎨 Example Code (Hinglish Comments)

```tsx
function HomeScreen({ navigation }) {
  return (
    <View>
      <Text>🏠 Home Screen</Text>
      <Button
        title="Go to Profile with Params"
        onPress={() =>
          navigation.navigate('Profile', { user: 'Kaushik', age: 24 })
        }
      />
    </View>
  );
}

function ProfileScreen({ route, navigation }) {
  // 📥 Params receive
  const { user, age } = route.params || {};

  return (
    <View>
      <Text>👤 Profile Screen</Text>
      <Text>Name: {user}</Text>
      <Text>Age: {age}</Text>

      {/* 🔄 Update params */}
      <Button
        title="Update Age"
        onPress={() => navigation.setParams({ age: age + 1 })}
      />

      {/* 🔙 Back */}
      <Button title="Go Back" onPress={() => navigation.goBack()} />
    </View>
  );
}
```

---

## 📊 Params Summary Table

| 🧩 Action       | 🔍 Usage                    | 🖼️ | Meaning        |
| --------------- | --------------------------- | --- | -------------- |
| Send → Navigate | `navigate('Screen',{id:1})` | 🧭  | Jump + send    |
| Send → Push     | `push('Screen',{id:1})`     | ➕   | Add + send     |
| Send → Replace  | `replace('Screen',{id:1})`  | 🔄  | Replace + send |
| Receive         | `route.params.id`           | 📦  | Access data    |
| Optional        | `route.params?.id`          | ❓   | Safe access    |
| Default         | `route.params?.id ?? 0`     | 🎯  | Fallback       |
| Update          | `setParams({id:2})`         | ✍️  | Change params  |
| Effect          | Screen re-render            | 🔁  | Auto update    |

---

## 🧠 Mental Model (Yaad Rakhne Ka Formula)

> **Navigate = Send**
> **Route = Receive**
> **SetParams = Update**

---

> ✅ **Best Practice:**
> Params ko sirf **UI-level data** ke liye use karo. Heavy state ke liye **Context / Redux / Zustand** better hai.

Happy Navigating 🚀📱
