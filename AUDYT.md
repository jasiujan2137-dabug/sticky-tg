# Audyt kodu Sticky TG

Data: 22 października 2026 r.

## Co sprawdzono

- Składnię `src/main.js` (kontrola `node --check`).
- Poprawność składni JSON w `package.json`.
- Czy identyfikatory elementów używane w `src/main.js` istnieją w `index.html` i czy nie powtarzają się w HTML.
- Konfigurację Vite i Cloudflare Workers Static Assets.
- Przepływ: wybór pliku → inicjalizacja FFmpeg → odczyt długości → ekstrakcja klatek → ramka/cień → kompresja → podgląd i pobranie.
- Pagedoll: element jest dostępny przy użyciu klawiatury, ma etykiety dostępności, można otworzyć/zamknąć dymek i ukryć maskotkę; animacja szanuje `prefers-reduced-motion`.

## Zmiany i poprawki

1. Loader FFmpeg korzysta z wersjonowanego builda ESM, zgodnego z Vite. Najpierw próbuje bezpośrednich adresów CDN; potem robi próbę przez Blob URL. W razie problemu próbuje drugiego CDN. Komunikat błędu zachowuje szczegóły każdej próby.
2. Usunięto `@ffmpeg/core` z zależności npm, ponieważ aplikacja wczytuje ten pakiet z CDN i nie importuje go z `node_modules`. Unika to niepotrzebnego pobierania dużego pliku WASM podczas instalacji.
3. Zachowano przetwarzanie w przeglądarce, bez wysyłania źródłowego wideo do serwera.
4. Dodano `.gitignore` dla zależności, buildów i lokalnych plików środowiskowych.
5. Dodano pagedolla w postaci wektorowego SVG, dymek, przycisk zamykania, responsywne rozmiary i ograniczenie animacji dla osób preferujących mniej ruchu.

## Sprawdzenia, których nie udało się wykonać

Nie udało się wykonać `npm install` ani `npm run build`, ponieważ środowisko audytu nie ma dostępu do rejestru npm. Nie wykonano rzeczywistej konwersji w przeglądarce ani wdrożenia na Cloudflare. Dlatego nie można zagwarantować, że każdy format MOV i każdy przeglądarkowy worker FFmpeg zadziała na docelowym hostingu. Po wgraniu projektu wymagany jest test na stronie wdrożonej na Cloudflare.

## Uwaga dotycząca repozytorium

Repozytorium `jasiujan2137-dabug/sticky-tg` było puste w chwili kontroli. Ta paczka zawiera kompletny projekt przygotowany do wgrania do katalogu głównego tego repozytorium; nie została automatycznie opublikowana w GitHubie.

## Licencje zależności

Przed publicznym rozpowszechnieniem sprawdź i zachowaj wymagane informacje licencyjne zależności, szczególnie silnika `@ffmpeg/core`, którego metadane pakietu wskazują licencję GPL-2.0-or-later. Ten audyt nie jest poradą prawną.
