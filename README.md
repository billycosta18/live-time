[README.md](https://github.com/user-attachments/files/33654843/README.md)
# Sygnalizator zajętości

Prosta strona: duże światło **zielone (WOLNE)** / **czerwone (ZAJĘTE)**.
Przełączasz na jednym komputerze — drugi od razu to pokazuje. Działa dla
każdego, bez logowania. Hostowane na GitHub Pages, synchronizacja przez
darmowy Firebase.

## Co musisz zrobić raz (ok. 5 minut)

### 1. Załóż darmową bazę Firebase
1. Wejdź na https://console.firebase.google.com/ i zaloguj się kontem Google.
2. Kliknij **Add project** / **Dodaj projekt**, podaj dowolną nazwę
   (np. `sygnalizator`), klikaj dalej (Google Analytics możesz wyłączyć).
3. W menu po lewej: **Build → Realtime Database → Create Database**.
   - Wybierz lokalizację (np. europe-west1).
   - Przy regułach wybierz **Start in test mode** → Enable.
     (Test mode = publiczny odczyt/zapis. Dla takiego sygnalizatora to OK.)
4. Jeszcze konfiguracja strony: **ikona koła zębatego → Project settings →**
   przewiń do **Your apps →** kliknij ikonę `</>` (Web).
   - Podaj nazwę (np. `sygnalizator`), **Register app**.
   - Firebase pokaże obiekt `firebaseConfig` z wartościami
     (apiKey, authDomain, databaseURL, projectId...). Skopiuj je.

### 2. Wklej dane do `index.html`
Otwórz `index.html`, znajdź sekcję **KONFIGURACJA** i wstaw swoje wartości
zamiast `WKLEJ_...`:

```js
var firebaseConfig = {
  apiKey: "TwójApiKey",
  authDomain: "twój-projekt.firebaseapp.com",
  databaseURL: "https://twój-projekt-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "twój-projekt"
};
```
> Ważne: skopiuj dokładnie `databaseURL` z Firebase — bywa z końcówką
> `.firebaseio.com` albo `.firebasedatabase.app`, zależnie od regionu.

### 3. Wrzuć na GitHub i włącz stronę
1. Na https://github.com załóż nowe repozytorium (np. `sygnalizator`),
   zaznacz **Public**.
2. **Add file → Upload files** → wrzuć `index.html` (i ten `README.md`).
   Commit.
3. **Settings → Pages →** w sekcji *Build and deployment* ustaw
   **Source: Deploy from a branch**, Branch: `main` / `/root`. Save.
4. Po chwili GitHub pokaże adres w stylu
   `https://twój-login.github.io/sygnalizator/`.

### 4. Gotowe
Otwórz ten adres na obu komputerach. Przełącz światło na jednym —
drugi zmieni kolor w ułamku sekundy.

## Uwagi
- Jeśli chcesz kilka niezależnych sygnalizatorów, zmień wartość
  `KANAL` w `index.html` na różne (np. `sala1/stan`, `sala2/stan`).
- Test mode w Firebase po ~30 dniach potrafi wygasić reguły. Jeśli po
  miesiącu przestanie działać, wejdź w Realtime Database → Rules i ustaw:
  ```json
  { "rules": { ".read": true, ".write": true } }
  ```
