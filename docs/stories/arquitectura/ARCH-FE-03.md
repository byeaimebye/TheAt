# ARCH-FE-03 — Configurar navegación con React Navigation

**Estado:** TODO
**Depende de:** ARCH-FE-02

---

## Objetivo

Tener el esqueleto de navegación completo: Auth, Coach y Atleta, con pantallas placeholder en cada tab.

---

## Tareas

- [ ] Instalar React Navigation:
  ```bash
  npm install @react-navigation/native @react-navigation/native-stack @react-navigation/bottom-tabs
  npx expo install react-native-screens react-native-safe-area-context
  ```
- [ ] Crear `AuthNavigator.tsx` con pantallas:
  - `WelcomeScreen`
  - `LoginScreen`
  - `RegisterScreen`
  - `RoleSelectionScreen`
- [ ] Crear `CoachNavigator.tsx` con 5 tabs:
  - Home · Atletas · Comunidad · Calendario · Configuración
- [ ] Crear `AthleteNavigator.tsx` con 5 tabs:
  - Home · Coach · Calendario · Comunidad · Configuración
- [ ] Crear `RootNavigator.tsx`:
  - Sin sesión → `AuthNavigator`
  - Sesión de coach → `CoachNavigator`
  - Sesión de atleta → `AthleteNavigator`
- [ ] Cada pantalla placeholder muestra solo su nombre centrado

---

## App.tsx base

```typescript
import { NavigationContainer } from '@react-navigation/native'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import { RootNavigator } from './src/navigation/RootNavigator'

const queryClient = new QueryClient()

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <NavigationContainer>
        <RootNavigator />
      </NavigationContainer>
    </QueryClientProvider>
  )
}
```

---

## Criterios para marcar como DONE

- [ ] Cambiando el estado de `authStore` se puede ver cada navigator
- [ ] Las 5 tabs del coach se ven correctamente
- [ ] Las 5 tabs del atleta se ven correctamente
- [ ] La app no crashea al navegar entre tabs
