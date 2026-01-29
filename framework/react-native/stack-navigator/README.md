# 📚 Stack.Navigator – Deep Dive Cheat Sheet

> **React Navigation (Native Stack)** ka complete, clean, **UI-friendly Markdown reference**. Ye file tum directly GitHub / Notion / Docs me use kar sakte ho.

---

## 🏗️ Core Props

| 🏷️ Prop           | 🔍 Description                             | 🎯 Example                              | 🖼️ |
| ------------------ | ------------------------------------------ | --------------------------------------- | --- |
| `initialRouteName` | App start hone par kaunsa screen open hoga | `initialRouteName="Home"`               | 🚪  |
| `screenOptions`    | Sab screens ke liye common options         | `screenOptions={{ headerShown:false }}` | ⚙️  |
| `id`               | Navigator ka unique identifier             | `id="root-stack"`                       | 🆔  |

---

## 🎨 Header & Screen Styling Props

| 🏷️ Prop              | 🔍 Description            | 🎯 Example                     | 🖼️ |
| --------------------- | ------------------------- | ------------------------------ | --- |
| `headerShown`         | Header show / hide        | `headerShown:false`            | 👀  |
| `headerTitle`         | Custom title              | `headerTitle:"Profile"`        | 📝  |
| `headerTitleAlign`    | Title alignment           | `"center"`                     | 📍  |
| `headerStyle`         | Header background styling | `{ backgroundColor:"purple" }` | 🎨  |
| `headerTintColor`     | Text & icon color         | `"white"`                      | 🎭  |
| `headerTitleStyle`    | Title text styling        | `{ fontSize:20 }`              | ✨   |
| `headerBackTitle`     | Back button text          | `"Back"`                       | 🔙  |
| `headerBackVisible`   | Back button hide/show     | `false`                        | 👈  |
| `headerTransparent`   | Transparent header        | `true`                         | 🧊  |
| `headerShadowVisible` | Shadow / border toggle    | `false`                        | ☁️  |

---

## 🎭 Screen Presentation & Animation

| 🏷️ Prop                  | 🔍 Description       | 🎯 Example     | 🖼️ |
| ------------------------- | -------------------- | -------------- | --- |
| `presentation`            | Screen style         | `"modal"`      | 🎬  |
| `animation`               | Transition animation | `"fade"`       | 🎞️ |
| `animationTypeForReplace` | Replace animation    | `"push"`       | 🔄  |
| `gestureEnabled`          | iOS back swipe       | `true`         | ✋   |
| `gestureDirection`        | Swipe direction      | `"horizontal"` | ↔️  |

---

## 📦 State, Performance & Memory

| 🏷️ Prop                  | 🔍 Description                     | 🎯 Example | 🖼️ |
| ------------------------- | ---------------------------------- | ---------- | --- |
| `detachPreviousScreen`    | Previous screen unmount            | `true`     | 🗑️ |
| `freezeOnBlur`            | Screen inactive par freeze         | `true`     | ❄️  |
| `keyboardHandlingEnabled` | Keyboard resize handling (Android) | `false`    | ⌨️  |

---

## 📱 Status Bar & Platform Specific

| 🏷️ Prop                   | 🔍 Description        | 🎯 Example   | 🖼️ |
| -------------------------- | --------------------- | ------------ | --- |
| `statusBarStyle`           | Status bar text color | `"light"`    | 🌙  |
| `statusBarHidden`          | Status bar hide       | `true`       | 🙈  |
| `statusBarAnimation`       | Status bar transition | `"slide"`    | 🎥  |
| `statusBarColor`           | Android status bar bg | `"black"`    | 🖤  |
| `fullScreenGestureEnabled` | iOS full swipe        | `true`       | 📲  |
| `orientation`              | Screen orientation    | `"portrait"` | 🔄  |

---

## ⚡ Complete Example (Production Style)

```tsx
<Stack.Navigator
  initialRouteName="Home"
  screenOptions={{
    headerShown: true,
    headerStyle: { backgroundColor: "purple" },
    headerTintColor: "white",
    headerTitleAlign: "center",
    presentation: "modal",
    animation: "slide_from_right",
    gestureEnabled: true,
    gestureDirection: "horizontal",
    detachPreviousScreen: false,
    freezeOnBlur: false,
    statusBarStyle: "light",
    fullScreenGestureEnabled: true,
    orientation: "portrait",
  }}
>
  <Stack.Screen
    name="Home"
    component={HomeScreen}
    options={{ headerTitle: "🏠 Home" }}
  />
  <Stack.Screen
    name="Profile"
    component={ProfileScreen}
    options={{ headerTitle: "👤 Profile", headerBackVisible: true }}
  />
</Stack.Navigator>
```

---

## 🚀 Quick Mental Model

* 🏗️ **Navigator Level** → Common behavior
* 🎨 **Screen Options** → UI consistency
* 🎭 **Presentation** → UX feel (modal / card)
* 📦 **Performance** → Memory + freeze
* 📱 **Platform** → iOS / Android polish

---

> ✅ **Tip:** Real apps me `screenOptions` minimal rakho, screen-specific options `Stack.Screen` me do.

Happy Navigating 🧭🔥
