# Habla Fluido

App Flutter para aprender inglés con un tutor de IA: oído, pronunciación, lectura, escritura y conversación, con repetición espaciada (SM-2) y un proxy Node que protege la llave de la IA.

Desarrollo Móvil Integral · UTNG

## App
```bash
flutter create . --project-name habla_fluido --platforms=android
flutter pub get
flutter test
flutter run                      # usa el tutor simulado (sin internet ni costo)
```

### Permisos de Android
En `android/app/src/main/AndroidManifest.xml`, dentro de `<manifest>`:
```xml
<uses-permission android:name="android.permission.RECORD_AUDIO"/>
<uses-permission android:name="android.permission.INTERNET"/>
```
y dentro del bloque `<queries>`:
```xml
<intent><action android:name="android.speech.RecognitionService"/></intent>
<intent><action android:name="android.intent.action.TTS_SERVICE"/></intent>
```

## Proxy de IA (opcional)
```bash
cd proxy
node --test
export ANTHROPIC_API_KEY=tu_llave    # Windows: set ANTHROPIC_API_KEY=tu_llave
node server.js
```
Luego en la app:
```bash
flutter run --dart-define=TUTOR_URL=https://tu-servidor.com/tutor
```
La llave nunca va en la app ni en Git.

## Estructura
- `lib/dominio`: reglas, comparador, SM-2, progreso, plan diario, contratos
- `lib/datos`: tutor simulado y HTTP, voz real y simulada, almacén
- `lib/presentacion`: ViewModels y pantallas
- `test`: pruebas de la app
- `proxy`: servidor Node con prompt, validación y límite de uso
