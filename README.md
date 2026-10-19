# Renowacja_motocykla

Aplikacja do prowadzenia renowacji motocykla SHL M04:
- status prac i plan etapów,
- weryfikacja części z katalogu SHL 125 (1953) z rysunkami,
- lista zakupów,
- etykiety Dymo na torebki.

Całość to jeden plik `index.html`. Nie ma serwera ani kompilacji, a aplikacja działa także offline.

## Zawartość

| Plik | Do czego |
|---|---|
| `index.html` | aplikacja (z katalogiem części i rysunkami) |
| `data/renowacja_motocykla_dane.json` | stan startowy. Ładuje się przy pierwszym otwarciu na nowym urządzeniu, jeśli synchronizacja nie jest włączona |
| `.nojekyll` | wyłącza Jekyll na GitHub Pages |

## Uruchomienie na GitHub Pages

1. Utwórz repozytorium **`Renowacja_motocykla`** i wrzuć do niego zawartość tego folderu.
2. Wejdź w Settings → Pages → *Deploy from a branch* → `main` / `/ (root)`.
3. Po około minucie aplikacja będzie pod adresem `https://<login>.github.io/Renowacja_motocykla/`.

Strona na GitHub Pages jest publiczna, dlatego dane trzymasz osobno, w prywatnym repozytorium (opis niżej).

## Praca na kilku urządzeniach (synchronizacja)

Stan aplikacji zapisuje się w pliku `renowacja_motocykla_dane.json` w **prywatnym** repozytorium danych. Dokumenty (PDF, skany) trafiają do katalogu `pliki/` w tym samym repozytorium.

1. Utwórz prywatne repozytorium **`Renowacja_motocykla_dane`**. Zaznacz „Add a README”, żeby powstała gałąź `main`.
2. Utwórz token: GitHub → Settings → Developer settings → **Fine-grained personal access tokens** → *Generate new token*.
   - Repository access: *Only select repositories* → `Renowacja_motocykla_dane`
   - Permissions → Repository → **Contents: Read and write**
3. W aplikacji wejdź w Panel administracyjny → **Dane i synchronizacja**. Wpisz login, `Renowacja_motocykla_dane` i token, potem kliknij **Połącz i synchronizuj**.
4. Powtórz krok 3 na telefonie i na drugim komputerze.

Jak działa synchronizacja:
- Przy otwarciu aplikacja pobiera najnowszy stan.
- Zmiany wysyłają się automatycznie około 4 sekund po edycji.
- Bez internetu zmiany czekają i wysyłają się po powrocie połączenia.
- Scalanie działa per projekt: wygrywa nowsza wersja. Jeśli ten sam projekt edytujesz jednocześnie na dwóch urządzeniach, zostaną zmiany z urządzenia, które zapisało później.
- Token jest zapisany tylko w przeglądarce danego urządzenia i nie trafia do repozytorium.

## Kopia zapasowa bez GitHub

W Panel administracyjny → Dane i synchronizacja:
- **Zapisz plik JSON** — zapisuje cały stan, opcjonalnie razem z dokumentami.
- **Wczytaj plik i scal / zastąp** — przywraca stan z pliku albo przenosi go na inne urządzenie.

Zapisany plik możesz też podmienić w `data/renowacja_motocykla_dane.json`. Będzie wtedy stanem startowym dla nowych urządzeń.

## Drukowanie etykiet Dymo

Otwórz listę części i kliknij ikonę drukarki przy części albo „Etykiety” przy zespole. W oknie drukowania ustaw:
- drukarkę DYMO,
- rozmiar papieru zgodny z etykietą (np. 99012 / 11352),
- marginesy: brak,
- skalę 100%.

## Ograniczenia

- Podgląd w claude.ai nie pozwala drukować, zapisywać plików ani łączyć się z GitHub. Do tego używaj wersji z GitHub Pages albo pliku `index.html` otwartego lokalnie.
- API GitHub przyjmuje pliki do 100 MB, więc bardzo duże skany lepiej podzielić.
