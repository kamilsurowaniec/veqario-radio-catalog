# Atrybucje — VEQARIO testowy katalog radia

## Dane lokalizacyjne: GeoNames

Współrzędne geograficzne i przypisanie miast do województw w
`radio/stations.json` pochodzą z bazy **GeoNames**.

- Źródło: <https://www.geonames.org/>
- Eksport danych: <https://download.geonames.org/export/dump/>
- Licencja: **Creative Commons Attribution 4.0 International (CC BY 4.0)**
- Treść licencji: <https://creativecommons.org/licenses/by/4.0/>

Dane GeoNames są udostępniane „tak jak są" (*as is*), bez gwarancji
poprawności ani aktualności. Zostały użyte wyłącznie na etapie budowania
katalogu (build-time) do rozwiązania nazw miast na współrzędne; aplikacja
VEQARIO nie odpytuje GeoNames w czasie działania.

Publikacja tego katalogu (lub danych z niego pochodnych) zawierającego
współrzędne z GeoNames wymaga **zachowania powyższej atrybucji i odnośnika
do licencji**. Ten plik ją realizuje.

## Logotypy

W tej wersji katalogu **nie opublikowano żadnego logotypu**. Katalogi
`radio/logos/groups/` i `radio/logos/streams/` są puste, a pole `logo`
w `radio/stations.json` nie jest ustawione dla żadnego wpisu.

Powód: logotypy stacji radiowych są znakami towarowymi ich nadawców i nie
znaleziono dla nich jednoznacznej licencji zezwalającej na redystrybucję.
Aplikacja używa własnego neutralnego placeholdera.

Każdy logotyp dodany w przyszłości zostanie tu wymieniony wraz ze źródłem,
licencją i odnośnikiem do treści licencji.

## Strumienie radiowe

Strumienie wskazywane przez `radio/streams.json` należą do swoich nadawców.
VEQARIO ich nie hostuje ani nie redystrybuuje i nie rości sobie do nich
żadnych praw — katalog zawiera wyłącznie odnośniki do publicznie dostępnych
endpointów wskazywanych przez oficjalne strony lub oficjalne playery nadawców.
Nazwy stacji i nadawców użyto wyłącznie w celu identyfikacji.
