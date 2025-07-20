# NetTurm - Android WebView Application

Это Android-приложение создано для удобного доступа к веб-интерфейсу через WebView с поддержкой сохранения сессии и загрузки файлов.

## Требования

- Android Studio или командная строка с установленным Gradle
- JDK 17 или новее
- Android SDK
- Устройство с Android 12.0 (API level 31) или новее

## Сборка приложения

### Debug версия (для тестирования)

Debug версия автоматически подписывается debug-ключом и готова к установке на устройство для тестирования.

```bash
./gradlew assembleDebug
```

APK файл будет создан в:
```
app/build/outputs/apk/debug/app-debug.apk
```

### Release версия (без подписи)

```bash
./gradlew assembleRelease
```

Неподписанный APK будет создан в:
```
app/build/outputs/apk/release/app-release-unsigned.apk
```

### Создание своего ключа для подписи (keystore)

1. Создайте keystore с помощью keytool:
```bash
keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-alias
```

2. Добавьте информацию о ключе в `app/build.gradle.kts`:
```kotlin
android {
    signingConfigs {
        create("release") {
            storeFile = file("path/to/my-release-key.jks")
            storePassword = "your_store_password"
            keyAlias = "my-alias"
            keyPassword = "your_key_password"
        }
    }
    
    buildTypes {
        release {
            signingConfig = signingConfigs.getByName("release")
        }
    }
}
```

3. Соберите подписанную release версию:
```bash
./gradlew assembleRelease
```

Подписанный APK будет создан в:
```
app/build/outputs/apk/release/app-release.apk
```

## Установка APK на устройство

1. Скопируйте APK файл на ваше Android устройство
2. На устройстве откройте файл менеджер и найдите скопированный APK
3. Нажмите на APK файл для начала установки
4. Если появится предупреждение, разрешите установку из неизвестных источников
5. Следуйте инструкциям установщика

## Разработка

Приложение использует:
- WebView для отображения веб-интерфейса
- CookieManager для сохранения сессии
- WebChromeClient для поддержки загрузки файлов

## Поддержка

При возникновении проблем, пожалуйста, создайте Issue в репозитории проекта.
