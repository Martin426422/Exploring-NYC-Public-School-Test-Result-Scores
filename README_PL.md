# Analiza wyników SAT szkół publicznych NYC (Python / Pandas)

## Przegląd
SAT składa się z trzech części: czytanie, matematyka i pisanie — każda maksymalnie 800 punktów (łącznie 2400 w tym zbiorze). Projekt analizuje wyniki SAT szkół publicznych NYC, aby wesprzeć decydentów, badaczy, administrację i rodziców.

Kluczowe pytania:
1. Które szkoły mają najlepsze wyniki z matematyki?
2. Jakie są Top‑10 szkół pod względem łącznego wyniku SAT?
3. Która dzielnica ma największe odchylenie standardowe łącznego wyniku SAT?

---

## Dane
- Plik: `schools.csv`
- Kolumny:
  - `school_name` — nazwa szkoły
  - `borough` — dzielnica NYC
  - `average_math`, `average_reading`, `average_writing` — wyniki SAT

---

## Technologia
- Python 3.x
- pandas
- Jupyter Notebook

---

## Uruchomienie
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install pandas jupyter
jupyter notebook
```

---

## Kroki analizy
```python
import pandas as pd
schools = pd.read_csv("schools.csv")

# Najlepsza matematyka
best_math = schools[schools["average_math"] > 800 * 0.8][["school_name", "average_math"]].sort_values("average_math", ascending=False)

# Top‑10 łączny SAT
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
top10 = schools[["school_name", "total_SAT"]].sort_values("total_SAT", ascending=False).head(10)

# Największe odchylenie w dzielnicach
boroughs = schools.groupby("borough")["total_SAT"].agg(["count", "mean", "std"]).round(2)
```

---

## Przykładowe wyniki
- Najlepsza matematyka: Stuyvesant (754), Bronx Science (714), Staten Island Tech (711)
- Top‑10 łączny SAT: Stuyvesant (2144), Bronx Science (2041), Staten Island Tech (2041)
- Największe odchylenie: Manhattan (~230.29)

---

## Licencja
MIT License © 2025 Martin Karwacki
