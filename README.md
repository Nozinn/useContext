# ⚛️ React useContext Hook

## 📌 Что такое useContext?
`useContext` — это хук React, который позволяет получать доступ к данным из **Context API** напрямую, без передачи props через каждую вложенность (избегаем *props drilling*).

---

## 🔑 Зачем нужен?
- Упрощает работу с данными, которые используются во многих компонентах  
- Делает код чище и короче  
- Удобен для глобальных данных: 🔐 авторизация, 🎨 тема, 🌍 язык и др.

---

## 🛠 Пример использования

### 1. Создание контекста
```jsx
import { createContext } from "react";

export const UserContext = createContext();
2. Обёртка в Provider
import React, { useState } from "react";
import { UserContext } from "./UserContext";
import Profile from "./Profile";

const App = () => {
  const [user, setUser] = useState("Nozina");

  return (
    <UserContext.Provider value={{ user, setUser }}>
      <h1>App Component</h1>
      <Profile />
    </UserContext.Provider>
  );
};

export default App;

3. Получение данных через useContext
import React, { useContext } from "react";
import { UserContext } from "./UserContext";

const Profile = () => {
  const { user, setUser } = useContext(UserContext);

  return (
    <div>
      <h2>Profile Component</h2>
      <p>User: {user}</p>
      <button onClick={() => setUser("Sabrina")}>Change User</button>
    </div>
  );
};

export default Profile;

🖼 Визуализация
❌ Без useContext (prop drilling)
App → Header → Navbar → Profile (props.user)

✅ С useContext
App (Provider)
 └── Profile (useContext)

✅ Когда использовать

Нужно передавать одни и те же данные в разные компоненты

Чтобы убрать цепочку props

Для глобального состояния приложения

⚠️ Когда НЕ стоит использовать

Данные нужны только в одном-двух компонентах

Сложное состояние → лучше Redux / Zustand

📚 Полезные ссылки

Документация useContext

Context API

🎯 Лучшие практики

Храните только то, что нужно в контексте (избегайте лишних ререндеров).

Разделяйте контексты (например, ThemeContext, AuthContext).

Используйте useMemo, если передаёте в контекст сложные объекты или функции.
