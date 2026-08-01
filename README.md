# 💉 VacunaRegistro MX

**Sistema Digital de Cartilla de Vacunación — México**

Aplicación móvil desarrollada en React Native con Expo que digitaliza la cartilla de vacunación de los ciudadanos mexicanos. Permite a los pacientes consultar su historial de vacunas mediante un código QR vinculado a su CURP, y al personal de salud registrar y consultar expedientes de forma segura.

---

## ✨ Funcionalidades

### Para Pacientes
- Acceso con CURP (18 caracteres)
- Visualización de la cartilla de vacunación digital en modo solo lectura
- Código QR personal generado a partir de la CURP
- Modal de QR a pantalla completa con aumento automático de brillo para facilitar el escaneo
- Tarjetas de vacuna expandibles con enfermedades que previene, dosis, frecuencia, lote y unidad médica

### Para Personal de Salud
- Login con correo institucional y contraseña
- **Pestaña Registrar** — identificación del paciente por escaneo de QR o CURP manual, con formulario para agregar vacunas al expediente
- **Pestaña Consultar** — directorio completo de pacientes con filtros por nombre, municipio y edad
- **Pestaña Perfil** — información del personal, cambio de contraseña y botón de alerta de posible brote epidémico con doble confirmación

---

## 🛠 Tecnologías

| Tecnología | Uso |
|---|---|
| React Native + Expo | Framework principal |
| Expo Camera | Escaneo de códigos QR |
| Expo Brightness | Control de brillo para el modal de QR |
| Expo Notifications | Notificación local de alerta de brote |
| React Navigation | Stack Navigator + Bottom Tabs |
| react-native-qrcode-svg | Generación de códigos QR |
| EAS Build | Compilación en la nube (preview y producción) |

---

## 📁 Estructura del Proyecto

```
vacuna-registro/
├── App.js
├── app.json
├── eas.json
└── src/
    ├── constants/
    │   └── colors.js              # Paleta de colores del sistema
    ├── data/
    │   ├── patients.js            # Mock de pacientes + helpers de fecha/edad
    │   ├── staff.js               # Mock de personal de salud
    │   └── vaccines.js            # Catálogo de vacunas con enfermedades y frecuencia
    ├── components/
    │   ├── VaccineRow.jsx         # Tarjeta expandible de vacuna
    │   └── PatientInfoCard.jsx    # Tarjeta de datos generales del paciente
    ├── screens/
    │   ├── HomeScreen.jsx
    │   ├── PatientCurpScreen.jsx
    │   ├── PatientCardScreen.jsx
    │   ├── StaffLoginScreen.jsx
    │   └── staff/
    │       ├── RegisterTab.jsx
    │       ├── ConsultTab.jsx
    │       └── ProfileTab.jsx
    └── navigation/
        ├── AppNavigator.jsx       # Stack raíz
        └── StaffTabs.jsx          # Bottom tabs del personal
```

---

## 🚀 Instalación y Ejecución

### Requisitos previos
- Node.js 18+
- Expo CLI
- Cuenta en [expo.dev](https://expo.dev)

### Clonar e instalar

```bash
git clone https://github.com/J-Cazz/App-Registro-Vacuna.git
cd vacuna-registro
npm install
```

### Instalar dependencias de Expo

```bash
npx expo install @react-navigation/native @react-navigation/native-stack @react-navigation/bottom-tabs
npx expo install react-native-screens react-native-safe-area-context
npx expo install react-native-qrcode-svg react-native-svg
npx expo install expo-camera
npx expo install expo-brightness
npx expo install expo-notifications
```

### Correr en desarrollo

```bash
npx expo start
```

Escanea el QR con la app **Expo Go** en tu dispositivo, o presiona `a` para Android emulator / `i` para iOS simulator.

---

## 📦 Build de Preview

### 1. Instalar EAS CLI e iniciar sesión

```bash
npm install -g eas-cli
eas login
eas build:configure
```

### 2. Generar APK para Android

```bash
eas build --profile preview --platform android
```

### 3. Generar build para iOS

```bash
eas build --profile preview --platform ios
```

> El build de iOS requiere una cuenta de **Apple Developer Program**.

---

## 🔐 Cuentas de Demostración

### Pacientes (ingresar con CURP)

| Nombre | CURP |
|---|---|
| Luis Alberto Gómez Núñez | `GOML990312HNLMNS04` |
| María Guadalupe Sarabia García | `SAGM010815MNLRLS08` |
| José Hernández Reyes | `REHJ850623HNLLRN07` |
| Tania Díaz Morales | `DIMT150901MNLZRN04` |

### Personal de Salud

| Correo | Contraseña |
|---|---|
| ana.garcia@salud.gob.mx | salud2024 |
| marco.ruiz@salud.gob.mx | salud2024 |

---

## 🔌 Integración con Sistema Central

Los datos actualmente viven dentro de la app (modo demostración). Cuando se desarrolle el sistema administrador central, los únicos archivos a modificar son:

- `src/data/patients.js` — reemplazar `PATIENTS` por llamadas `fetch()` a la API
- `src/data/staff.js` — reemplazar `STAFF` por el endpoint de autenticación
- `src/screens/staff/RegisterTab.jsx` — reemplazar `patientsStore` por mutaciones a la API

El resto de la app no requiere cambios.

---

## ⚠️ Consideraciones para Producción

- Las contraseñas están en texto plano en el mock. En producción deben almacenarse como hashes (bcrypt) y la autenticación debe realizarse con JWT desde el backend.
- Implementar expiración de sesión y refresh tokens.
- Las alertas de brote deben autenticarse y registrarse en el servidor.
- Toda comunicación con el sistema central debe ser por HTTPS/TLS.

---

## 📄 Licencia

Este proyecto fue desarrollado como parte del sistema de salud digital de México.
Secretaría de Salud · Gobierno de México.
