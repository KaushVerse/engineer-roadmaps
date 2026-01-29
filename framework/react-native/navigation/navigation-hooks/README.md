# 📚 All React Navigation Hooks – Deep Dive (with Icons)

> **React Navigation Hooks** ka complete, Hinglish + icon-based reference. Ye canvas **daily development + interview + debugging** ke liye perfect hai.

---

## 🪝 All Navigation Hooks at a Glance

| 🪝 Hook              | 🔍 Purpose                | 🖼️ | Example                |
| -------------------- | ------------------------- | --- | ---------------------- |
| `useNavigation`      | Navigation object access  | 🧭  | `navigate(), goBack()` |
| `useRoute`           | Current route info        | 🛤️ | `route.params`         |
| `useFocusEffect`     | Focus pe effect run       | 👀  | API fetch              |
| `useIsFocused`       | Screen focused? (boolean) | 🎯  | Video pause            |
| `useNavigationState` | Navigation state access   | 🗺️ | Debug stack            |
| `useScrollToTop`     | Tab press → scroll top    | ⬆️  | Feed reset             |
| `useLinkTo`          | Deep linking navigation   | 🔗  | URL based nav          |
| `useTheme`           | Theme colors access       | 🎨  | Dark / Light UI        |

---

## 🧭 `useNavigation`

```tsx
import { useNavigation } from '@react-navigation/native';

function MyButton() {
  const navigation = useNavigation();
  return (
    <Button
      title="Go Profile"
      onPress={() => navigation.navigate('Profile', { id: 99 })}
    />
  );
}
```

**Use when:** component directly screen prop nahi receive kar raha ho.

---

## 🛤️ `useRoute`

```tsx
import { useRoute } from '@react-navigation/native';

function ProfileScreen() {
  const route = useRoute();
  return <Text>Profile ID: {route.params?.id}</Text>;
}
```

**Use when:** params ya route name access karna ho.

---

## 👀 `useFocusEffect`

```tsx
import { useFocusEffect } from '@react-navigation/native';
import { useCallback } from 'react';

function FeedScreen() {
  useFocusEffect(
    useCallback(() => {
      console.log('🔵 Screen Focused → Fetch Data');
      return () => console.log('⚪ Screen Blurred → Cleanup');
    }, [])
  );

  return <Text>Feed</Text>;
}
```

**Better than:** `addListener('focus')` for most cases.

---

## 🎯 `useIsFocused`

```tsx
import { useIsFocused } from '@react-navigation/native';

function VideoPlayer() {
  const isFocused = useIsFocused();
  return <Text>{isFocused ? '▶️ Playing' : '⏸️ Paused'}</Text>;
}
```

**Best for:** media, animations, timers.

---

## 🗺️ `useNavigationState`

```tsx
import { useNavigationState } from '@react-navigation/native';

function Debugger() {
  const index = useNavigationState(state => state.index);
  return <Text>Current Stack Index: {index}</Text>;
}
```

**Use when:** debugging or analytics.

---

## ⬆️ `useScrollToTop`

```tsx
import { useScrollToTop } from '@react-navigation/native';
import { FlatList } from 'react-native';
import { useRef } from 'react';

function Feed() {
  const ref = useRef(null);
  useScrollToTop(ref);

  return (
    <FlatList
      ref={ref}
      data={[1, 2, 3]}
      renderItem={({ item }) => <Text>{item}</Text>}
    />
  );
}
```

**UX pattern:** Instagram-style scroll to top.

---

## 🔗 `useLinkTo`

```tsx
import { useLinkTo } from '@react-navigation/native';

function DeepLinkButton() {
  const linkTo = useLinkTo();
  return (
    <Button
      title="Go to Profile"
      onPress={() => linkTo('/profile/42')}
    />
  );
}
```

**Used in:** deep linking, web URLs.

---

## 🎨 `useTheme`

```tsx
import { useTheme } from '@react-navigation/native';

function ThemedText() {
  const { colors } = useTheme();
  return <Text style={{ color: colors.primary }}>Hello Themed World</Text>;
}
```

**Use when:** dark/light mode support.

---

## 🧠 Mental Model (Interview Gold ✨)

* **Hooks = cleaner alternative to props + listeners**
* **Focus-based hooks > lifecycle hacks**
* **State hooks = debugging tools**

---

## ✅ Best Practices

* Prefer **hooks** over `navigation.addListener`
* `useFocusEffect` > `useEffect` for screen lifecycle
* Avoid heavy logic in `useNavigationState`

Happy Hooking 🪝🚀
