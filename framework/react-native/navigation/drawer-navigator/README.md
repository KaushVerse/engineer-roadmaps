# 📂 Drawer Navigator – createDrawerNavigator (Deep Dive)

> **React Navigation Drawer** ka complete, visual + Hinglish reference. Ye canvas **real apps, large layouts, aur interview prep** ke liye perfect hai.

---

## 🤔 What is a Drawer Navigator?

Drawer ek **side-panel navigation** deta hai jo screen ke **left / right se slide** hota hai.

* 📱 Mobile apps → usually **left drawer**
* 🖥️ Tablet / Web → **permanent drawer** bhi use hota hai

---

## ⚙️ Installation

```bash
npm install @react-navigation/drawer
npm install react-native-gesture-handler react-native-reanimated
```

---

## 📚 Basic Example

```tsx
import { createDrawerNavigator } from '@react-navigation/drawer';
import { NavigationContainer } from '@react-navigation/native';
import { Ionicons } from '@expo/vector-icons';

const Drawer = createDrawerNavigator();

function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator
        screenOptions={{
          drawerType: 'front',
          drawerPosition: 'left',
          headerShown: true,
          drawerStyle: { backgroundColor: '#fff', width: 240 },
        }}
      >
        <Drawer.Screen
          name="Home"
          component={HomeScreen}
          options={{
            title: '🏠 Home',
            drawerIcon: ({ color, size }) => (
              <Ionicons name="home-outline" size={size} color={color} />
            ),
          }}
        />
        <Drawer.Screen
          name="Profile"
          component={ProfileScreen}
          options={{
            title: '👤 Profile',
            drawerIcon: ({ color, size }) => (
              <Ionicons name="person-outline" size={size} color={color} />
            ),
          }}
        />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

---

## 🎨 Drawer.Navigator Props

| 🧩 Prop            | 🔍 Description       | 🖼️  | Example                            |
| ------------------ | -------------------- | ---- | ---------------------------------- |
| `initialRouteName` | Default screen       | 🚪   | `"Home"`                           |
| `drawerPosition`   | Drawer side          | ⬅️➡️ | `left / right`                     |
| `drawerType`       | Drawer behavior      | 📂   | `front / back / slide / permanent` |
| `drawerStyle`      | Drawer styling       | 🎨   | `{ backgroundColor:'white' }`      |
| `overlayColor`     | Background dim color | 🌑   | `rgba(0,0,0,0.5)`                  |
| `swipeEnabled`     | Swipe gesture        | 👆   | `true / false`                     |
| `headerShown`      | Header visible       | 🔝   | `true / false`                     |
| `lazy`             | Lazy load screens    | 💤   | `true / false`                     |

---

## 🎨 Drawer.Screen → options

| 🧩 Option       | 🔍 Description    | 🖼️ | Example                 |
| --------------- | ----------------- | --- | ----------------------- |
| `title`         | Drawer item label | 🏷️ | `"Dashboard"`           |
| `drawerLabel`   | Custom label      | ✍️  | `'My Profile'`          |
| `drawerIcon`    | Drawer icon       | 🎨  | `({color}) => <Icon />` |
| `swipeEnabled`  | Per-screen swipe  | 👆  | `false`                 |
| `unmountOnBlur` | Blur pe unmount   | 🧹  | `true`                  |

---

## 📊 Drawer Actions

| 🧩 Action      | 🔍 Description    | 🖼️ | Example             |
| -------------- | ----------------- | --- | ------------------- |
| `openDrawer`   | Drawer open       | 📖  | `openDrawer()`      |
| `closeDrawer`  | Drawer close      | ❌   | `closeDrawer()`     |
| `toggleDrawer` | Toggle open/close | 🔄  | `toggleDrawer()`    |
| `jumpTo`       | Drawer item jump  | 🏃  | `jumpTo('Profile')` |

---

## 🏆 Deep Concepts (Must Know)

| 💡 Concept        | 🔍 Explanation               | 🖼️ |
| ----------------- | ---------------------------- | --- |
| Custom Drawer     | `drawerContent` se custom UI | 🎨  |
| Permanent Drawer  | Tablet / Web layouts         | 🖥️ |
| Nested Navigators | Drawer ke andar Stack / Tabs | 🏗️ |
| Gesture Control   | Per screen swipe enable      | 👆  |
| Overlay Effect    | Drawer open pe dim bg        | 🌑  |

---

## ⚡ Example – Custom Drawer Content

```tsx
<Drawer.Navigator
  drawerContent={(props) => <CustomDrawerContent {...props} />}
>
  <Drawer.Screen name="Home" component={HomeScreen} />
  <Drawer.Screen name="Settings" component={SettingsScreen} />
</Drawer.Navigator>

function CustomDrawerContent(props) {
  return (
    <DrawerContentScrollView {...props}>
      <DrawerItem
        label="💬 Messages"
        onPress={() => props.navigation.navigate('Messages')}
      />
      <DrawerItem
        label="⚙️ Settings"
        onPress={() => props.navigation.navigate('Settings')}
      />
    </DrawerContentScrollView>
  );
}
```

---

## 🧠 Mental Model (Interview Gold ✨)

* **Drawer** → Global navigation
* **Tabs** → Primary sections
* **Stack** → Page flow

> 🧩 Drawer + Tabs + Stack = most common production architecture

---

> ✅ **Best Practices:**
>
> * Drawer items **5–7 max** rakho
> * Drawer me deep screens mat rakho
> * Tablet/Web ke liye `drawerType:'permanent'`

Happy Sliding 📂🚀
