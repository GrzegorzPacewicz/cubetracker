# Cube Tracker

Tracker treningu speedcubingu (3x3 i inne konkurencje WCA) dla zawodników. PWA do codziennego odhaczania zadań z planu ułożonego przez trenera.

Wyrósł z [treningBLD](https://github.com/GrzegorzPacewicz/treningBLD) — ten sam silnik, inne szablony zadań i wygląd.

## Live

https://cubetracker.grzegorzpacewicz.pl

## Stack

- Vanilla JS/CSS/HTML, zero frameworków
- PWA (network-first service worker, cache tylko GET)
- PocketBase (`gp1.pecet.it`) — plan, postępy, auth

## Jak to działa

- Każdy zawodnik ma konto w kolekcji `users` (zakłada trener w panelu admina).
- Wszystkie rekordy mają pole `user`; reguły API (`user = @request.auth.id`) i filtr w aplikacji pokazują każdemu tylko jego dane. Te same kolekcje co treningBLD.
- Plan edytuje się w aplikacji, w **panelu planów** (po zalogowaniu na konto zawodnika):
  - **Warianty** — szablony tygodni (`weekly_variants`)
  - **Tydzień** — przypisanie wariantu do tygodnia (`weekly_schedule`)
  - **Zasady** — sekcja "Na co położyć nacisk" (`training_focus`)
  - **Zadania** — typy zadań i ich szczegóły (`task_templates`; do czasu dodania własnych używane są wbudowane szablony 3x3 z `app.js`)
  - edycja pojedynczego dnia — nadpisania (`training_overrides`)
- Start programu = najwcześniejszy dzień z postępem, a gdy go brak — pierwszy zaplanowany tydzień.

## Struktura plików

```
├── index.html      # Główna aplikacja
├── style.css       # Style (akcent: --accent)
├── app.js          # Logika UI + wbudowane szablony zadań
├── pocketbase.js   # Klient PocketBase (dane, auth, filtr po użytkowniku)
├── sw.js           # Service worker
├── manifest.json   # PWA manifest
├── icon.svg        # Ikona
└── test.js         # Testy: node test.js
```
