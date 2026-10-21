# Sticky TG — Vista Sticker Studio

Konwerter krótkich filmów MOV, MP4 i WebM do animowanego WEBM VP9 z kanałem alfa. Projekt używa Vite i FFmpeg WASM oraz ma dekoracyjnego pagedolla (niebieski kotek) w rogu strony.

## Uruchomienie lokalne

Wymagany Node.js LTS (18 lub nowszy; zalecany aktualny LTS).

```bash
npm install
npm run dev
```

Otwórz adres wyświetlony przez Vite.

## Test kompilacji

```bash
npm run build
npm run preview
```

## Wdrożenie na Cloudflare Workers Static Assets

```bash
npx wrangler login
npm run deploy
```

W panelu Cloudflare sprawdź, czy worker `sticky-tg` jest przypisany do tego repozytorium i czy po deployu aktywna jest najnowsza wersja. Samo założenie repozytorium GitHub nie przełącza automatycznie istniejącej domeny `*.workers.dev`.

## Jak działa FFmpeg

W przeglądarce FFmpeg ładuje się dopiero po kliknięciu „Konwertuj”. Kod próbuje wersjonowany build ESM z jsDelivr, a następnie unpkg; dla każdego źródła ma próbę bezpośredniego adresu oraz próbę przez Blob URL. To pomaga rozróżnić błędy CORS/importu od braku połączenia z CDN.

Plik wideo jest przetwarzany w przeglądarce i nie jest wysyłany do serwera. Pierwsze użycie wymaga pobrania plików silnika z CDN.

## Funkcje

- Wybór pliku MOV, MP4 lub WebM.
- Podgląd wideo.
- Włączana ramka, wybór koloru i grubości, regulowany cień.
- Eksport WEBM VP9 z kanałem alfa w rozmiarze 512 × 512, do 30 FPS i 3 sekund, z limitem 256 KiB.
- Pasek postępu, komunikaty błędów, anulowanie po zakończeniu bieżącego kroku.
- Pagedoll jako dekoracyjny kotek w prawym dolnym rogu; kliknięcie otwiera dymek, a × ukrywa maskotkę.
- Obsługa preferencji `prefers-reduced-motion` i widoku mobilnego.

## Ważne ograniczenia

- To projekt frontendowy; nie ma backendu ani wysyłania filmu na serwer.
- Przeglądarka musi obsługiwać moduły JavaScript, WebAssembly oraz Web Workers.
- Ostateczny plik należy sprawdzić w Telegramie. Akceptacja formatu zależy od zasad Telegrama oraz parametrów źródłowego wideo.

## Wgranie do pustego repozytorium GitHub

1. Rozpakuj ZIP na komputerze.
2. Otwórz puste repozytorium GitHub i wybierz **Add file → Upload files**.
3. Przeciągnij do okna GitHuba zawartość tego folderu: `index.html`, `package.json`, `vite.config.js`, `wrangler.toml`, `README.md`, `AUDYT.md`, `.gitignore` i folder `src`.
4. Zatwierdź przez **Commit changes**. Plik `package.json` ma być w głównym katalogu repozytorium, a nie w dodatkowym folderze `sticky-tg-pagedoll`.

Jeśli repozytorium jest połączone z Cloudflare, sprawdź ustawienia budowania i wdrożenia. Przy wdrażaniu z terminala użyj poleceń z sekcji Cloudflare powyżej.
