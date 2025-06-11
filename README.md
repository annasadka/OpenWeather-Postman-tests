# OpenWeather-Postman-tests

Przypadki testowe

## 1. Aktualna pogoda Warszawa

**Opis (PL):**  
Sprawdzenie, czy API zwraca aktualną temperaturę i nazwę miasta Warszawa.

**Description (EN):**  
Verify that the API returns the current temperature and the city name Warsaw.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.
- Sprawdź, czy kod odpowiedzi to 200.
- Zweryfikuj, czy pole `name` w odpowiedzi to `Warsaw`.
- Sprawdź, czy pole `main.temp` istnieje i jest liczbą.

<br><br>

## 2. Aktualna pogoda dla nieistniejącego miasta (Neverland)

**Opis (PL):**  
Sprawdzenie obsługi błędów dla fikcyjnego miasta Neverland.

**Description (EN):**  
Check error handling for a fictional city Neverland.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Neverland`.
- Sprawdź, czy kod odpowiedzi to 404 lub 400.
- Zweryfikuj, czy odpowiedź zawiera komunikat o błędzie (`message`).

<br><br>

## 3. Prognoza 5-dniowa dla poprawnego miasta

**Opis (PL):**  
Sprawdzenie, czy API zwraca prognozę 5-dniową dla Warszawy.

**Description (EN):**  
Verify that the API returns a 5-day forecast for Warsaw.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/forecast?q=Warsaw`.
- Sprawdź, czy kod odpowiedzi to 200.
- Zweryfikuj, czy w odpowiedzi znajduje się pole `list` (tablica prognoz).
- Sprawdź, czy pole `city.name` to `Warsaw`.

<br><br>

## 4. Walidacja danych o wietrze

**Opis (PL):**  
Sprawdzenie, czy API zwraca poprawne dane o sile i kierunku wiatru oraz czy wartości są w spodziewanym zakresie.

**Description (EN):**  
Verify that the API returns correct wind speed and direction data, and that values are within the expected range.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.
- Sprawdź, czy kod odpowiedzi to 200.
- Zweryfikuj, czy w odpowiedzi znajduje się obiekt `wind` z polami `speed` i `deg`.
- Sprawdź, czy `wind.speed` jest liczbą ≥ 0.
- Sprawdź, czy `wind.deg` jest liczbą z zakresu 0–360.

<br><br>

## 5. Walidacja wilgotności, ciśnienia i zachmurzenia

**Opis (PL):**  
Sprawdzenie, czy API zwraca dane o wilgotności, ciśnieniu i zachmurzeniu oraz czy wartości są logiczne.

**Description (EN):**  
Verify that the API returns humidity, pressure, and cloudiness data, and that the values are logical.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/weather?q=Warsaw`.
- Sprawdź, czy kod odpowiedzi to 200.
- Zweryfikuj obecność pól: `main.humidity`, `main.pressure`, `clouds.all`.
- Sprawdź, czy wilgotność (`main.humidity`) to liczba 0–100.
- Sprawdź, czy ciśnienie (`main.pressure`) to liczba > 800.
- Sprawdź, czy zachmurzenie (`clouds.all`) to liczba 0–100.

<br><br>

## 6. Aktualna pogoda i prognoza – porównanie temperatur dla Warszawy

**Opis (PL):**  
Pobierz aktualną temperaturę z endpointu /weather i zapisz ją. Następnie pobierz temperaturę z najbliższej prognozy z endpointu /forecast i porównaj obie wartości. Wypisz obie temperatury w konsoli.

**Description (EN):**  
Fetch the current temperature from the /weather endpoint and save it. Then fetch the temperature from the nearest forecast from the /forecast endpoint and compare both values. Print both temperatures in the console.

**Kroki testowe / Test steps:**
-Wykonaj zapytanie GET do /data/2.5/weather?q=Warsaw.
-W zakładce Tests zapisz temperaturę do zmiennej środowiskowej current_temp.
-Wykonaj zapytanie GET do /data/2.5/forecast?q=Warsaw.
-W zakładce Tests pobierz temperaturę z pierwszego elementu tablicy list.main.temp.
-Porównaj ją ze zmienną current_temp.
-Wypisz obie temperatury w konsoli.

<br><br>

## 7. Prognoza – Warszawa – Porównanie danych z różnych endpointów

**Opis (PL):**  
Porównaj temperaturę z endpointu `/forecast` z wcześniej zapisaną temperaturą z `/weather` dla Warszawy. Wypisz w konsoli aktualną i prognozowaną temperaturę.

**Description (EN):**  
Compare the temperature from the `/forecast` endpoint with the previously saved temperature from `/weather` for Warsaw. Print both current and forecasted temperatures in the console and check if the difference does not exceed 3°C.

**Kroki testowe / Test steps:**
- Wykonaj zapytanie GET do `/data/2.5/forecast?q=Warsaw`.
- Pobierz temperaturę z pierwszego elementu tablicy `list[0].main.temp`.
- Porównaj tę wartość z temperaturą zapisaną w zmiennej środowiskowej `current_temp`.
- Wypisz obie temperatury w konsoli Postmana.
