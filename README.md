# Rejestr nazw serwerów lewicowYT

Rejestr zamienia pseudodomenę serwera społeczności z końcówką `.lewyt` (np. `lewica-krakow.lewyt`) na jego adres `.onion` lub HTTPS. Aplikacja lewicowYT pobiera stąd podpisane pliki przez sieć Tor, więc nie trzeba przepisywać długich adresów.

## Dodanie serwera

1. Do `manifest.json` swojego serwera dodaj pole potwierdzające, że go kontrolujesz:
   ```json
   "dnsClaim": "github:TWOJ-LOGIN"
   ```
2. Otwórz zgłoszenie **[Dodaj serwer](../../issues/new/choose)** i wypełnij formularz.
3. Automat sprawdzi zgłoszenie przez Tor (zwykle w ciągu kilkunastu minut), odpowie w zgłoszeniu i je zamknie. Po przyjęciu pole `dnsClaim` można usunąć.

Zmianę adresu i usunięcie wpisu zgłasza się tak samo, odpowiednim formularzem. Może to zrobić tylko konto, które dodało wpis.

## Zasady

- Nazwa to pseudodomena `<nazwa>.lewyt`. Końcówkę `.lewyt` można w formularzu pominąć — zostanie dopisana. Część przed kropką: 3–40 znaków, małe litery `a–z`, cyfry i pojedyncze myślniki. Nazwy łudząco podobne do istniejących (np. `0` zamiast `o`) oraz nazwy zastrzeżone nie są przyjmowane.
- Adres `.onion` (Tor v3) lub publiczna domena HTTPS. Domyślny port to 2137.
- Jeden adres może należeć tylko do jednego wpisu. Jedno konto może mieć najwyżej 3 wpisy.
- Konto GitHub musi istnieć od co najmniej 30 dni.
- Serwer, który nie odpowiada przez 3 dni, dostaje ostrzeżenie w swoim zgłoszeniu. Po 14 dniach wpis jest usuwany.

## Pliki

| Plik | Zawartość |
|---|---|
| `rejestr/indeks.json` | Podpisany indeks: wersja, data ważności i skrót SHA-256 każdego pliku litery |
| `rejestr/<znak>.<skrót>.json` | Wpisy, których nazwa zaczyna się od danego znaku (a–z, 0–9) |
| `podglad/rejestr.json` | Czytelna lista wszystkich wpisów (tylko do podglądu) |

Pliki w katalogu `rejestr/` tworzy wyłącznie automat. Aplikacja sprawdza podpis indeksu przypiętym kluczem oraz skrót każdego pliku litery, więc ręczna zmiana pliku zostanie odrzucona.

Aplikacja pobiera tylko indeks i plik pierwszej litery szukanej nazwy. Nie trzeba pobierać całej listy, a GitHub nie widzi, o który serwer chodzi.
