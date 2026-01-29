# 🚀 Tab Navigator – Bottom Tabs & Material Top Tabs (Deep Dive)

> **React Navigation Tabs** ka complete, visual + Hinglish reference. Ye canvas **real apps, interviews, aur production code** ke liye ready hai.

---

## 🏷️ Types of Tab Navigators

| 🏷️ Type                                                | 🔍 Description                      | 📱 Example Apps     | 🖼️ |
| ------------------------------------------------------- | ----------------------------------- | ------------------- | --- |
| **Bottom Tabs** (`createBottomTabNavigator`)            | Bottom pe icons + labels            | Instagram, WhatsApp | ⬇️  |
| **Material Top Tabs** (`createMaterialTopTabNavigator`) | Top pe swipeable tabs (Material UI) | Play Store, Gmail   | ⬆️  |

---

## ⚙️ Installation

```bash
npm install @react-navigation/bottom-tabs

# Material Top Tabs
npm install @react-navigation/material-top-tabs react-native-tab-view
```

---

## 📚 Basic Example – Bottom Tabs

```tsx
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { NavigationContainer } from '@react-navigation/native';
import { Ionicons } from '@expo/vector-icons';

const Tab = createBottomTabNavigator();

function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator
        screenOptions={({ route }) => ({
          tabBarIcon: ({ focused, color, size }) => {
            let iconName;
            if (route.name === 'Home') {
              iconName = focused ? 'home' : 'home-outline';
            } else if (route.name === 'Settings') {
              iconName = focused ? 'settings' : 'settings-outline';
            }
            return <Ionicons name={iconName} size={size} color={color} />;
          },
          tabBarActiveTintColor: 'tomato',
          tabBarInactiveTintColor: 'gray',
          headerShown: false,
        })}
      >
        <Tab.Screen name="Home" component={HomeScreen} />
        <Tab.Screen name="Settings" component={SettingsScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

---

## 🎨 Important Props – `Tab.Navigator`

| 🧩 Prop                   | 🔍 Description    | 🖼️ | Example                       |
| ------------------------- | ----------------- | --- | ----------------------------- |
| `screenOptions`           | Global tab config | ⚙️  | icons, labels                 |
| `initialRouteName`        | Default open tab  | 🚪  | `"Home"`                      |
| `tabBarStyle`             | Tab bar styling   | 🎨  | `{ backgroundColor:'black' }` |
| `tabBarShowLabel`         | Label show/hide   | 🏷️ | `false`                       |
| `tabBarActiveTintColor`   | Active color      | 🎯  | `'tomato'`                    |
| `tabBarInactiveTintColor` | Inactive color    | ⚪   | `'gray'`                      |
| `tabBarBadge`             | Badge on tab      | 🔴  | `3`                           |

---

## 🎨 Important Props – `Tab.Screen` → `options`

| 🧩 Prop            | 🔍 Description | 🖼️ | Example                     |
| ------------------ | -------------- | --- | --------------------------- |
| `title`            | Tab title      | 🏷️ | `'My Home'`                 |
| `tabBarIcon`       | Custom icon    | 🎨  | `({color}) => <Icon />`     |
| `tabBarBadge`      | Badge count    | 🔴  | `99`                        |
| `tabBarBadgeStyle` | Badge styling  | 🎨  | `{ backgroundColor:'red' }` |
| `tabBarLabel`      | Custom label   | ✍️  | `'Feed'`                    |

---

## 🏆 Deep Concepts (Must Know)

| 💡 Concept               | 🔍 Explanation                                | 🖼️ |
| ------------------------ | --------------------------------------------- | --- |
| Lazy Loading             | `lazy:true` → tab open hone par mount         | 💤  |
| Unmount on Blur          | `unmountOnBlur:true` → tab change pe unmount  | 🧹  |
| Custom Tab Bar           | `tabBar={(props) => <MyTabBar {...props} />}` | 🎨  |
| Nested Navigators        | Tab ke andar Stack / Drawer                   | 🏗️ |
| Swipe Enabled (Top Tabs) | Top tabs swipe support                        | 👆  |

---

## 📊 Lifecycle Events in Tabs

| 🔔 Event       | 🔍 Description      | 🖼️ | Use Case        |
| -------------- | ------------------- | --- | --------------- |
| `focus`        | Tab active hota hai | 👀  | Data refresh    |
| `blur`         | Tab inactive        | 🏃  | Pause / cleanup |
| `tabPress`     | Tab press           | 👆  | Scroll to top   |
| `tabLongPress` | Long press          | ✋   | Context menu    |

---

## ⚡ Example – Badge + Custom Icon

```tsx
<Tab.Screen
  name="Messages"
  component={MessagesScreen}
  options={{
    tabBarBadge: 5,
    tabBarIcon: ({ color }) => (
      <Ionicons name="chatbubble" size={24} color={color} />
    ),
  }}
/>
```

---

## 🧠 Mental Model (Interview Gold ✨)

* **Bottom Tabs** → Primary app sections
* **Top Tabs** → Category / filter views
* **Tab switch** → focus / blur events
* **Heavy state** → unmountOnBlur avoid karo

---

> ✅ **Best Practice:**
>
> * Bottom tabs me **3–5 tabs** ideal hote hain
> * Top tabs me swipe UX ke liye `lazy:true` use karo
> * Har tab ke andar Stack Navigator rakhna common pattern hai

Happy Tabbing 🏷️🚀
