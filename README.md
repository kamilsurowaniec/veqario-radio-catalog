# VEQARIO — testowy katalog radia internetowego

Publiczny katalog stacji radiowych używany do **testów drogowych** aplikacji
VEQARIO (dashboard OBD2/GPS dla Skody Octavii II).

> **To nie jest wydanie produkcyjne.** Katalog powstał po to, żeby sprawdzić
> odtwarzanie radia w samochodzie. Zawartość może się zmienić lub zniknąć
> w dowolnym momencie, bez zapowiedzi i bez zachowania zgodności wstecznej.

## Ważne zastrzeżenia

- **URL-e strumieni w `radio/streams.json` są jawne i publiczne.** To świadoma
  decyzja na czas testów drogowych — **nie** jest to bezpieczny ani prywatny
  hosting. Docelowo linki zostaną schowane za mechanizmem `ticketApi`.
- **Strumienie należą do swoich nadawców.** VEQARIO ich nie hostuje, nie
  redystrybuuje dźwięku i nie rości sobie do nich żadnych praw. Katalog zawiera
  wyłącznie odnośniki do publicznie dostępnych strumieni nadawców.
- **Żadna stacja nie jest prawnie zatwierdzona.** Endpointy potwierdzono na
  oficjalnych stronach lub w oficjalnych playerach nadawców, ale pełny przegląd
  regulaminów nie został zakończony.
- Jeżeli jesteś nadawcą i chcesz, aby Twoja stacja została usunięta z tego
  katalogu — zgłoś to przez GitHub Issues tego repozytorium. Usuniemy wpis.

## Struktura katalogu

```
.nojekyll                  wyłącza przetwarzanie Jekyll na GitHub Pages
README.md                  ten plik
ATTRIBUTION.md             wymagane atrybucje źródeł danych
radio/
  stations.json            publiczny katalog metadanych (schema v2) — BEZ URL-i
  streams.json             jeden wspólny manifest odtwarzania (manifestVersion 1)
  radio-config.json        konfiguracja klienta (configVersion 1)
  logos/groups/<groupId>.webp    logotypy grup (tylko zatwierdzone assety)
  logos/streams/<streamId>.webp  logotypy stacji (tylko zatwierdzone assety)
```

Klient startuje od `radio/radio-config.json` i rozwiązuje pozostałe ścieżki
**względnie** do niego:

- `catalogPath` → `stations.json` — metadane stacji, grup i lokalizacji.
  Ten plik **nigdy** nie zawiera URL-i odtwarzania.
- `resolver.uri` → `streams.json` — mapa `streamId → primaryUrl + fallbackUrls`
  (maksymalnie 5 fallbacków, wyłącznie HTTPS).
- `logoBasePath` → `logos/` — prefiks ścieżek do logotypów.

`catalogRevision` w `streams.json` i `radio-config.json` musi być równe
`revision` w `stations.json`. Zbiór `streamId` w obu plikach jest identyczny.

## Grupy regionalne i kanały tematyczne

Przynależność stacji do sieci regionalnej wyraża **wyłącznie pole `groupId`**
przy streamie — grupa nie przechowuje listy swoich dzieci. Każdy stream
regionalny ma komplet: `city`, `voivodeship`, `latitude`, `longitude`.

Grupa może wskazać `nationalFallbackStreamId` — ogólnopolski stream tej samej
sieci, bez miasta i bez współrzędnych. Klient używa go, gdy nie potrafi wybrać
najbliższego regionu.

**Kanały tematyczne** (np. listy przebojów, kanały gatunkowe i dekadowe znanych
sieci) są w tym katalogu **samodzielnymi stacjami**: mają `groupId: null`, nie
mają lokalizacji i nie biorą udziału w wyborze najbliższego regionu.

## Zgłaszanie niedziałających stacji

Otwórz **GitHub Issues** w tym repozytorium i podaj `streamId` z `stations.json`
oraz krótki opis objawu. Nie podawaj w zgłoszeniu żadnych danych osobowych.

## Generowanie

Pliki w `radio/` są generowane przez narzędzia administratora
(`tool/radio_catalog/`) z prywatnego źródła spoza tego repozytorium.
**Nie edytuj ich ręcznie** — każda zmiana zostanie nadpisana przy kolejnym
buildzie.

---

**English summary:** public road-test radio catalog for the VEQARIO car
dashboard. Not a production release. The stream URLs in `radio/streams.json`
are deliberately public for testing — this is not secure hosting. All streams
belong to their broadcasters; VEQARIO only links to publicly reachable
endpoints and claims no rights to them. Broadcasters who want an entry removed
can open a GitHub Issue.
