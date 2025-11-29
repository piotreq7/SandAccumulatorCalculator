# Symulator Akumulatora Piaskowego 🔥

Aplikacja webowa do symulacji systemu magazynowania energii termicznej w piasku z instalacji fotowoltaicznej.

## 📑 Spis treści

1. [🚀 Szybki start - JAK UŻYĆ?](#-szybki-start---jak-użyć)
2. [📋 Opis techniczny](#-opis)
3. [🔬 Model fizyczny](#-model-fizyczny)
4. [📊 Przykładowe wyniki](#-przykładowe-wyniki)
5. [💬 FAQ - Najczęściej zadawane pytania](#-najczęściej-zadawane-pytania-faq)
6. [📊 Przykłady praktyczne](#-przykłady-praktyczne)
7. [🎯 Typowe scenariusze](#-typowe-scenariusze-użycia)
8. [🔧 Rozwiązywanie problemów](#-rozwiązywanie-problemów)

---

## 🚀 Szybki start - JAK UŻYĆ?

### Krok 1: Otwórz aplikację
```
Otwórz plik akumulator_piaskowy.html w przeglądarce (Chrome, Firefox, Edge)
```

### Krok 2: Przygotuj plik CSV z danymi produkcji
Potrzebujesz pliku CSV z danymi z Twojej instalacji fotowoltaicznej. Plik musi zawierać kolumny:

**Przykładowy plik `produkcja.csv`:**
```csv
time,daily-production
2024-01-01,8.5
2024-01-02,12.3
2024-01-03,6.7
2024-01-04,15.2
```

**Kolumny (może być dowolna z tych nazw):**
- Data: `time`, `Time`, `data`
- Produkcja: `daily-production`, `Daily-Production`, `Produkcja-dziś(kWh)`

### Krok 3: Skonfiguruj zbiornik

#### 3.1 Wybierz kształt:
- **Prostopadłościan** - prostsze w budowie
- **Walec** - ~10% mniejsze straty ciepła

#### 3.2 Ustaw wymiary:

**Dla prostopadłościanu:**
- Długość: np. 2m
- Szerokość: np. 2m  
- Wysokość: np. 2m
- → Objętość: 8 m³ → Pojemność: ~17 kWh

**Dla walca:**
- Promień: np. 1m
- Wysokość: np. 2.5m
- → Objętość: ~7.85 m³ → Pojemność: ~17 kWh

#### 3.3 Ustaw grubość izolacji:
- **50-100mm** - podstawowa izolacja, większe straty
- **200mm** (domyślne) - dobry kompromis
- **300-500mm** - bardzo dobre magazynowanie, małe straty
- ⚠️ Podstawa będzie automatycznie **4× grubsza** (musi wytrzymać ciężar piasku)

#### 3.4 Ustaw maksymalną temperaturę:
- **400-500°C** - łatwiejsza realizacja, mniejsza pojemność
- **600°C** (domyślne) - typowa dla akumulatorów piaskowych
- **700-1000°C** - większa pojemność, trudniejsza technicznie

#### 3.5 Skalowanie produkcji PV (opcjonalnie):
- **100%** - pełna produkcja z pliku CSV
- **50%** - symulacja połowy mocy (np. dla instalacji 6 kW zamiast 12 kW)
- **150%** - symulacja większej instalacji

### Krok 4: Wczytaj dane
1. Kliknij przycisk **"📁 Wybierz plik CSV"**
2. Wybierz swój plik z danymi produkcji
3. ✅ Poczekaj na komunikat z podsumowaniem

### Krok 5: Analizuj wykresy

Po wczytaniu danych zobaczysz **4 wykresy**:

📊 **1. Stan akumulatora (kWh)**
- Pokazuje ile energii jest zmagazynowane w każdym dniu
- Czy zbiornik się przepełnia?
- Czy wystarczy pojemność?

📉 **2. Straty energii (kWh/dzień)**
- Ile energii ucieka przez izolację każdego dnia
- Im wyższe słupki, tym gorsze magazynowanie
- Zależą od temperatury i grubości izolacji

🌡️ **3. Temperatura piasku (°C)**
- **Pomarańczowa linia** - temperatura w centrum (najgoręcej)
- **Zielona linia** - średnia temperatura w całym piasku
- **Niebieska linia** - temperatura przy ściankach (najzimniej)
- Im większe odstępy między liniami = większe straty

📈 **4. Produkcja energii (kWh)**
- Twoje dane wejściowe z pliku CSV
- Dla porównania z stanem akumulatora

### Krok 6: Eksperymentuj!

Zmień parametry i zobacz różnice:
- ✏️ Zwiększ izolację → mniejsze straty
- ✏️ Zmień kształt na walec → mniejsze straty
- ✏️ Zwiększ temperaturę max → większa pojemność
- ✏️ Zwiększ wymiary → większa pojemność

Po każdej zmianie aplikacja automatycznie przeliczy symulację!

---

## 📋 Opis

Akumulator piaskowy to innowacyjny system przechowywania energii termicznej. Nadwyżki energii z paneli fotowoltaicznych są przekształcane w ciepło i magazynowane w piasku, który może osiągnąć temperatury do 1000°C. Zgromadzone ciepło może być następnie wykorzystane do ogrzewania lub produkcji energii elektrycznej.

### Dlaczego piasek?
- ✅ Tani i powszechnie dostępny
- ✅ Wytrzymuje bardzo wysokie temperatury (>1000°C)
- ✅ Bezpieczny (nie pali się, nie wybucha)
- ✅ Duża pojemność cieplna
- ✅ Długa żywotność (nie degraduje się)

### Jak działa magazynowanie?
1. **Nadmiar energii z PV** → przekształcany w ciepło (grzałki elektryczne)
2. **Ciepło grzeje piasek** → temperatura rośnie do 600°C
3. **Piasek magazynuje energię** → przez dni/tygodnie
4. **Oddawanie ciepła** → do systemu grzewczego lub do produkcji prądu

---

## 🔬 Model fizyczny

### Parametry piasku (medium magazynujące):
- **Przewodność cieplna λ**: 0.27 W/(m·K)
- **Gęstość**: 1600 kg/m³
- **Ciepło właściwe**: 0.835 kJ/(kg·K)
- **Zakres temperatur**: 20°C - 600°C (konfigurowalny)

### Izolacja (wełna mineralna):
- **Przewodność cieplna λ**: 0.04 W/(m·K)
- **~6.75× lepsza** niż piasek
- **Podstawa 4× grubsza** (materiał konstrukcyjny nośny)

### Model strat cieplnych:
```
Q = ΔT / R_total

gdzie:
R_total = R_piasek + R_izolacja
R = grubość / (λ × powierzchnia)
```

- Straty obliczane jako **szeregowe połączenie** oporności termicznych
- Podstawa i ściany jako **równoległe** ścieżki strat
- Uwzględnia **gradient temperatury** w piasku

### Gradient temperatury:
- **W centrum**: temperatura maksymalna
- **Przy ściankach**: temperatura niższa (zależy od strat)
- **Rozkład**: paraboliczny
- **Wzór**: T_avg = (2×T_center + T_wall) / 3

## 📁 Format danych wejściowych

Plik CSV z danymi produkcji z instalacji PV (12 kW):

```csv
time,daily-production
2024-01-01,8.5
2024-01-02,12.3
2024-01-03,6.7
...
```

**Wymagane kolumny:**
- `time` lub `Time` - data
- `daily-production` lub `Daily-Production` - produkcja dzienna w kWh

## 🚀 Użytkowanie

1. Otwórz plik `akumulator_piaskowy.html` w przeglądarce
2. Skonfiguruj parametry zbiornika:
   - Wybierz kształt (prostopadłościan/walec)
   - Ustaw wymiary
   - Ustaw grubość izolacji
   - Ustaw maksymalną temperaturę
3. Kliknij **"📁 Wybierz plik CSV"**
4. Wybierz plik z danymi produkcji
5. Analizuj wykresy i statystyki

## 📈 Przykładowe wyniki

### Zbiornik 1×1×1m (1 m³), izolacja 200mm, temp. max 600°C:

**Pojemność**: ~2.17 kWh

**Dla instalacji 12 kW przez rok:**
- Całkowita produkcja: ~3000 kWh/rok
- Średnie straty: ~1-3 kWh/dzień
- Wykorzystanie: 20-40% produkcji może być zmagazynowane

### Porównanie kształtów (ta sama objętość):

**Prostopadłościan 1×1×1m:**
- Powierzchnia: 6 m²
- Straty: większe

**Walec ⌀1.13m × 1m:**
- Powierzchnia: ~5.54 m²
- Straty: ~10% mniejsze (optymalna geometria)

## 🛠️ Technologie

- **HTML5** + **CSS3** - interfejs użytkownika
- **JavaScript** - logika symulacji
- **Chart.js** - wizualizacje wykresów
- **PapaParse** - parsowanie plików CSV

## 📐 Wzory i obliczenia

### Pojemność akumulatora:
```
E = m × c × ΔT / 3600
```
gdzie:
- m = objętość × gęstość [kg]
- c = ciepło właściwe piasku [kJ/(kg·K)]
- ΔT = T_max - 20°C [K]
- E = pojemność [kWh]

### Średnia droga ciepła przez piasek:

**Prostopadłościan:**
```
d = (długość + szerokość + wysokość) / 6
```

**Walec:**
```
d = (promień + wysokość/2) / 2
```

### Oporność termiczna:
```
R_piasek = d_piasek / (λ_piasek × A)
R_izolacja = d_izolacja / (λ_izolacja × A)
```

## 💡 Wskazówki

- **Większy zbiornik** = większa pojemność, ale wolniejsze nagrzewanie
- **Grubsza izolacja** = mniejsze straty, wyższy koszt
- **Walec** = lepsza efektywność niż prostopadłościan
- **Wyższa temp.** = większa pojemność, trudniejsza realizacja
- **Podstawa 4× grubsza** = musi przenieść ciężar piasku

## 📊 Statystyki po wczytaniu danych

Aplikacja wyświetla:
- Okres danych i czas trwania
- Kształt i wymiary zbiornika
- Objętość i pojemność
- Zakres temperatur
- Średnią drogę ciepła przez piasek
- Moc instalacji PV (nominalna i przeskalowana)
- Produkcję energii (przed i po skalowaniu)
- Straty cieplne (średnie i całkowite)
- Stan końcowy akumulatora

## 🔍 Przypadki użycia

1. **Optymalizacja wymiarów** - znajdź optymalny rozmiar dla swojej instalacji
2. **Porównanie izolacji** - sprawdź wpływ grubości izolacji na straty
3. **Test kształtów** - walec vs prostopadłościan
4. **Analiza temperatur** - wpływ temperatury max na pojemność
5. **Skalowanie instalacji** - symulacja różnych mocy PV

## ⚠️ Ograniczenia modelu

- Model uproszczony (rzeczywiste zachowanie może się różnić)
- Nie uwzględnia zmian wilgotności piasku
- Stała temperatura otoczenia (20°C)
- Jednolity materiał piasku
- Brak uwzględnienia efektów konwekcji
- Przewodność cieplna λ stała (w rzeczywistości zależy od temp.)

## 💬 Najczęściej zadawane pytania (FAQ)

### ❓ Dlaczego zbiornik się przepełnia?
**Odpowiedź:** Zbiornik ma za małą pojemność. Rozwiązania:
- Zwiększ wymiary zbiornika
- Zwiększ maksymalną temperaturę (np. z 600°C na 800°C)
- Zmniejsz skalowanie produkcji PV (jeśli testujesz scenariusze)

### ❓ Dlaczego straty są tak duże?
**Odpowiedź:** Słaba izolacja lub zbyt wysoka temperatura. Rozwiązania:
- Zwiększ grubość izolacji (np. z 200mm na 400mm)
- Zmień kształt na walec (10% mniejsze straty)
- Obniż maksymalną temperaturę (mniejsza różnica temp. = mniejsze straty)

### ❓ Jaki kształt wybrać?
**Odpowiedź:** 
- **Walec** - jeśli zależy Ci na wydajności (mniejsze straty ~10%)
- **Prostopadłościan** - jeśli liczy się łatwość budowy

### ❓ Jaka grubość izolacji jest optymalna?
**Odpowiedź:** 
- **200-300mm** - dobry kompromis koszt/efektywność
- Pamiętaj: podstawa będzie 4× grubsza (800-1200mm)

### ❓ Co oznaczają 3 linie na wykresie temperatury?
**Odpowiedź:**
- **Pomarańczowa (górna)** - temp. w centrum (najgoręcej)
- **Zielona (środkowa)** - średnia temp. całego piasku
- **Niebieska (dolna)** - temp. przy ściankach (najzimniej)
- Duże odstępy = duże straty przez piasek

### ❓ Dlaczego podstawa ma grubszą izolację?
**Odpowiedź:** Podstawa musi wytrzymać ciężar piasku (~1600 kg/m³). Dlatego używa się materiałów konstrukcyjnych (np. bloczki betonowe wypełnione izolacją) - stąd 4× większa grubość.

### ❓ Czy mogę użyć własnych danych z mojej instalacji PV?
**Odpowiedź:** TAK! Wyeksportuj dane do CSV z dwoma kolumnami:
- Data (time)
- Produkcja dzienna (daily-production) w kWh

### ❓ Co zrobić jeśli nie mam pliku CSV?
**Odpowiedź:** Musisz najpierw przygotować plik z danymi produkcji. Możesz:
- Pobrać dane z inwentera/falownika
- Użyć danych z systemu monitoringu (np. SolarEdge, Fronius)
- Stworzyć testowy plik CSV ręcznie

## 📊 Przykłady praktyczne

### Przykład 1: Mały domowy akumulator
```
Kształt: Prostopadłościan
Wymiary: 1m × 1m × 1m
Izolacja: 200mm (podstawa 800mm)
Temp. max: 600°C
Pojemność: ~2.17 kWh
```
**Dla kogo:** Małe instalacje ~3-5 kW, krótkoterminowe magazynowanie

### Przykład 2: Średni akumulator domowy
```
Kształt: Walec
Promień: 1.5m, Wysokość: 3m
Izolacja: 300mm (podstawa 1200mm)
Temp. max: 600°C
Pojemność: ~45 kWh
```
**Dla kogo:** Instalacje ~10-15 kW, magazynowanie na kilka dni

### Przykład 3: Duży akumulator
```
Kształt: Walec
Promień: 3m, Wysokość: 5m
Izolacja: 500mm (podstawa 2000mm)
Temp. max: 700°C
Pojemność: ~350 kWh
```
**Dla kogo:** Duże instalacje, długoterminowe magazynowanie energii

## 🎯 Typowe scenariusze użycia

### Scenariusz 1: "Czy moja instalacja 12 kW potrzebuje akumulatora?"
1. Wczytaj roczne dane produkcji
2. Zobacz wykres stanu akumulatora
3. Jeśli **często się przepełnia** → nie potrzebujesz większego
4. Jeśli **rzadko osiąga 50%** → możesz zmniejszyć lub zrezygnować

### Scenariusz 2: "Jaki rozmiar zbiornika wybrać?"
1. Zacznij od małego (1×1×1m)
2. Wczytaj dane i sprawdź stan końcowy
3. Jeśli zbiornik pełny → zwiększ wymiary o 50%
4. Powtarzaj aż znajdziesz optymalny rozmiar

### Scenariusz 3: "Opłaca się dodatkowa izolacja?"
1. Symuluj z izolacją 200mm → zapisz straty całkowite
2. Symuluj z izolacją 400mm → zapisz straty całkowite
3. Oblicz różnicę w stratach
4. Porównaj z kosztem dodatkowej izolacji

### Scenariusz 4: "Walec vs Prostopadłościan?"
1. Ustaw prostopadłościan (np. 2×2×2m)
2. Zapisz: straty całkowite, stan końcowy
3. Zmień na walec (r=1.26m, h=2m - ta sama objętość)
4. Porównaj wyniki (walec ~10% lepszy)

## 🔧 Rozwiązywanie problemów

### Problem: "Nie mogę wczytać pliku CSV"
**Rozwiązanie:**
1. Sprawdź czy plik ma rozszerzenie `.csv`
2. Otwórz plik w notatniku - sprawdź format
3. Upewnij się że są kolumny: `time` i `daily-production`
4. Zobacz konsolę przeglądarki (F12) - tam są szczegóły błędu

### Problem: "Wykresy nie wyświetlają się"
**Rozwiązanie:**
1. Odśwież stronę (F5)
2. Sprawdź czy masz połączenie z internetem (potrzebne do pobrania bibliotek)
3. Spróbuj innej przeglądarki (Chrome, Firefox)

### Problem: "Dziwne wartości na wykresach"
**Rozwiązanie:**
1. Sprawdź jednostki w pliku CSV (powinny być kWh, nie Wh)
2. Sprawdź czy skalowanie PV = 100%
3. Sprawdź czy wymiary są w metrach, nie centymetrach

## 📝 Licencja

Projekt edukacyjny - wolne użytkowanie.

## 👤 Autor

Symulator stworzony jako narzędzie do analizy systemu magazynowania energii termicznej.

---

**Data aktualizacji**: 2025-01-29
**Wersja**: 1.0
**Plik główny**: `akumulator_piaskowy.html`

## 🆘 Potrzebujesz pomocy?

1. Przeczytaj sekcję "FAQ" powyżej
2. Sprawdź "Rozwiązywanie problemów"
3. Otwórz konsolę przeglądarki (F12) - tam są szczegółowe logi

