# Symulator Akumulatora Piaskowego 🔥

Aplikacja webowa do symulacji systemu magazynowania energii termicznej w piasku z instalacji fotowoltaicznej.

## 📋 Opis

Akumulator piaskowy to innowacyjny system przechowywania energii termicznej. Nadwyżki energii z paneli fotowoltaicznych są przekształcane w ciepło i magazynowane w piasku, który może osiągnąć temperatury do 1000°C. Zgromadzone ciepło może być następnie wykorzystane do ogrzewania lub produkcji energii elektrycznej.

## ✨ Funkcje

### 🎛️ Konfiguracja systemu

- **Kształt zbiornika**: Wybór między prostopadłościanem a walcem
  - Prostopadłościan: długość × szerokość × wysokość
  - Walec: promień × wysokość (lepsza efektywność cieplna)

- **Wymiary**: Dowolne wymiary od 0.1m do 50m
  - Domyślnie: 1×1×1m

- **Izolacja**: Grubość izolacji 0-1000mm
  - Domyślnie: 200mm
  - Podstawa automatycznie 4× grubsza (konstrukcja nośna)

- **Temperatura maksymalna**: 100-1000°C
  - Domyślnie: 600°C
  - Wyższa temperatura = większa pojemność, trudniejsza realizacja

- **Skalowanie produkcji PV**: 0-200%
  - 100% = pełna moc z pliku CSV
  - 50% = symulacja mniejszej instalacji

## 📊 Wizualizacje

Aplikacja generuje 4 wykresy w czasie rzeczywistym:

1. **🔋 Stan akumulatora** - poziom zgromadzonej energii [kWh]
2. **📉 Straty energii** - dzienne straty przez izolację [kWh/dzień]
3. **🌡️ Temperatura piasku** - 3 krzywe:
   - Temperatura w centrum (max)
   - Średnia temperatura piasku
   - Temperatura przy ściankach (przed izolacją)
4. **📈 Produkcja energii** - dzienna produkcja z instalacji PV [kWh]

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

## 📝 Licencja

Projekt edukacyjny - wolne użytkowanie.

## 👤 Autor

Symulator stworzony jako narzędzie do analizy systemu magazynowania energii termicznej.

---

**Data aktualizacji**: 2025-01-29
**Wersja**: 1.0
**Plik główny**: `akumulator_piaskowy.html`

