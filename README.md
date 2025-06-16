# OpenWeather-Postman-tests
<br>

## Opis projektu
Projekt prezentuje przykładowe testy automatyczne API pogodowego OpenWeatherMap wykonane w Postmanie. Celem było przećwiczenie walidacji odpowiedzi API, obsługi błędów i porównania danych z różnych endpointów.
<br><br>

## Technologie
- Postman
- OpenWeatherMap API
<br>

## Dokumentacja API
[OpenWeatherMap API](https://openweathermap.org/api)
<br><br>

## Jak uruchomić testy?
1. Sklonuj repozytorium.
2. Zaimportuj plik kolekcji do Postmana.
3. Ustaw swój klucz API jako zmienną środowiskową `api_key`.
4. Uruchom testy ręcznie lub przez Collection Runner.
<br>

## Przypadki testowe

### 1. Aktualna pogoda Warszawa

**Opis:**  
Sprawdzenie, czy API zwraca aktualną temperaturę i nazwę miasta Warszawa.

**Kroki testowe:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.

**Oczekiwane rezultaty:**
- Kod odpowiedzi to **200**.
- W odpowiedzi pole `name` ma wartość **"Warsaw"**.
- W odpowiedzi pole `main.temp` istnieje i jest liczbą.

<br>

### 2. Aktualna pogoda dla nieistniejącego miasta (Neverland)

**Opis:**  
Sprawdzenie obsługi błędów dla fikcyjnego miasta Neverland.

**Kroki testowe:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Neverland`.
  
**Oczekiwane rezultaty:**
- Kod odpowiedzi to **404** lub **400**.
- W odpowiedzi znajduje się pole `message` z komunikatem o błędzie.

<br>

### 3. Prognoza 5-dniowa dla Warszawy

**Opis:**  
Sprawdzenie, czy API zwraca prognozę 5-dniową dla Warszawy.


**Kroki testowe:**
- Wykonaj zapytanie GET do `/data/2.5/forecast?q=Warsaw`.

**Oczekiwane rezultaty:**
- Kod odpowiedzi to **200**.
- W odpowiedzi znajduje się pole `list` będące tablicą prognoz.
- Pole `city.name` ma wartość **"Warsaw"**.

<br>

### 4. Walidacja danych o wietrze

**Opis:**  
Sprawdzenie, czy API zwraca poprawne dane o sile i kierunku wiatru oraz czy wartości są w spodziewanym zakresie.


**Kroki testowe:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.

**Oczekiwane rezultaty:**
- Kod odpowiedzi to **200**.
- W odpowiedzi znajduje się obiekt `wind` z polami `speed` i `deg`.
- `wind.speed` jest liczbą większą lub równą 0.
- `wind.deg` jest liczbą z zakresu 0–360.
  
<br>

### 5. Walidacja wilgotności, ciśnienia i zachmurzenia

**Opis:**  
Sprawdzenie, czy API zwraca dane o wilgotności, ciśnieniu i zachmurzeniu oraz czy wartości są logiczne.

**Kroki testowe:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.

**Oczekiwane rezultaty:**
- Kod odpowiedzi to **200**.
- W odpowiedzi znajduje się pole `main.humidity` (liczba 0–100).
- W odpowiedzi znajduje się pole `main.pressure` (liczba większa od 800).
- W odpowiedzi znajduje się pole `clouds.all` (liczba 0–100).

<br>

### 6. Aktualna pogoda i prognoza – porównanie temperatur dla Warszawy

**Opis:**  
Pobierz aktualną temperaturę z endpointu /weather i zapisz ją. Następnie pobierz temperaturę z najbliższej prognozy z endpointu /forecast i porównaj obie wartości. Wypisz obie temperatury w konsoli.

**Kroki testowe:**
1. Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw` i zapisz wartość `main.temp` do zmiennej środowiskowej `current_temp`.
2. Wykonaj zapytanie GET do `/data/2.5/forecast?q=Warsaw`.
3. Pobierz temperaturę z pierwszego elementu tablicy `list[0].main.temp`.
4. Wypisz w konsoli Postmana obie temperatury: aktualną i prognozowaną.


**Oczekiwane rezultaty:**
- Obie temperatury są widoczne w konsoli Postmana.


<br><br>


