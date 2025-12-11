# NYC Public Schools — SAT Performance Analysis (Python / Pandas)

## Overview
Every year, U.S. high school students take the SAT, a standardized test with three sections: Reading, Math, and Writing — each scored out of 800 points (maximum combined 2400 in this dataset). This project analyzes New York City (NYC) public school SAT performance to support stakeholders such as policy makers, researchers, school administrators, and parents.

Key questions:
1. Which NYC schools have the best math results?
2. What are the top 10 performing schools based on the combined SAT score?
3. Which borough has the largest standard deviation of the combined SAT score?

---

## Dataset
- File: `schools.csv`
- Columns:
  - `school_name` — school name
  - `borough` — NYC borough
  - `average_math`, `average_reading`, `average_writing` — SAT section scores

---

## Tech Stack
- Python 3.x
- pandas
- Jupyter Notebook

---

## Setup
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install pandas jupyter
jupyter notebook
```

---

## Core Analysis Steps
```python
import pandas as pd
schools = pd.read_csv("schools.csv")

# Best math results
best_math = schools[schools["average_math"] > 800 * 0.8][["school_name", "average_math"]].sort_values("average_math", ascending=False)

# Top 10 combined SAT
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
top10 = schools[["school_name", "total_SAT"]].sort_values("total_SAT", ascending=False).head(10)

# Borough with largest std deviation
boroughs = schools.groupby("borough")["total_SAT"].agg(["count", "mean", "std"]).round(2)
```

---

## Example Outputs
- Best Math: Stuyvesant High School (754), Bronx High School of Science (714), Staten Island Technical High School (711)
- Top 10 combined SAT: Stuyvesant (2144), Bronx Science (2041), Staten Island Tech (2041)
- Largest std deviation: Manhattan (~230.29)

---

## License
MIT License © 2025 Martin Karwacki
