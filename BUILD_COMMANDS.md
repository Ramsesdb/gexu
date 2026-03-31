# 🔧 Build Commands - Gexu

Guía rápida de comandos Gradle para compilar y probar Gexu.

---

## 🚀 APK para Pruebas en Teléfono (Óptimo)

### ⭐ Preview Build (Óptimo para Testing de Rendimiento)

```bash
# Build optimizado con firma debug (RECOMENDADO para probar en teléfono)
./gradlew :app:installPreview

# APK generado en:
# app/build/outputs/apk/preview/app-arm64-v8a-preview.apk
```

> [!TIP]
> **Preview** es un Release con firma debug: código optimizado con R8, sin logs excesivos, APK más pequeño (~40-60MB), y **máximo rendimiento**. Perfecto para testing real sin configurar keystore.

---

### Debug Build (Para desarrollo con logs)

```bash
# Build rápido sin optimización (para debugging)
./gradlew :app:assembleDebug

# APK generado en:
# app/build/outputs/apk/debug/app-arm64-v8a-debug.apk
```

### Instalar Directamente en el Dispositivo

```bash
# Preview (recomendado para rendimiento)
./gradlew :app:installPreview

# Debug (para desarrollo con logs)
./gradlew :app:installDebug

# O manualmente con ADB:
adb install -r app/build/outputs/apk/preview/app-arm64-v8a-preview.apk
```

> [!NOTE]
> El build `debug` compila más rápido pero **NO** aplica minificación (R8). El APK será más grande (~100-120MB) y el rendimiento será menor.

---

## 📦 Todos los Build Types

| Comando | Descripción | Uso |
|---------|-------------|-----|
| `assembleDebug` | Debug con logs y depuración | Desarrollo diario |
| `assembleRelease` | Release optimizado con R8 | Distribución |
| `assemblePreview` | Release con firma debug | Testing pre-release |
| `assembleFoss` | Sin servicios propietarios | F-Droid compatible |
| `assembleBenchmark` | Optimizado para profiling | Medición de rendimiento |

```bash
# Ejemplos:
./gradlew :app:assembleRelease
./gradlew :app:assemblePreview
./gradlew :app:assembleFoss
```

---

## 🧹 Comandos de Limpieza

```bash
# Limpiar todo el proyecto
./gradlew clean

# Limpiar y reconstruir
./gradlew clean :app:assembleDebug
```

---

## ✅ Verificación de Código (CI)

```bash
# Verificar formato de código (spotless/ktlint)
./gradlew spotlessCheck

# Aplicar formato automáticamente
./gradlew spotlessApply

# Ejecutar tests unitarios
./gradlew testDebugUnitTest
```

---

## 📲 Comandos ADB Útiles

```bash
# Listar dispositivos conectados
adb devices

# Instalar APK (reemplazar si existe)
adb install -r <path_to_apk>

# Desinstalar app
adb uninstall com.ramsesbr.gexu.debug

# Ver logs en tiempo real (filtrar por app)
adb logcat | findstr "gexu"

# Capturar logs completos
adb logcat -d > logcat.txt
```

---

## 🎯 Comandos Combinados (Copy-Paste Ready)

### Build + Install rápido
```powershell
./gradlew :app:installDebug
```

### Limpieza completa + Build
```powershell
./gradlew clean :app:assembleDebug
```

### Verificar formato + Build
```powershell
./gradlew spotlessApply :app:assembleDebug
```

### Build Release (para distribuir)
```powershell
./gradlew :app:assembleRelease
```

---

## 📁 Ubicación de APKs Generados

| Build Type | Ruta del APK |
|------------|--------------|
| Debug | `app/build/outputs/apk/debug/` |
| Release | `app/build/outputs/apk/release/` |
| Preview | `app/build/outputs/apk/preview/` |
| FOSS | `app/build/outputs/apk/foss/` |

> [!NOTE]
> El proyecto genera APKs por arquitectura (`arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64`) y uno universal. Para teléfonos modernos, usa `arm64-v8a`.

---

## 📋 Requisitos

- **JDK**: 17+
- **Android SDK**: API 26-35
- **NDK**: Incluido en el proyecto
- **Espacio en disco**: ~5GB para builds completos
