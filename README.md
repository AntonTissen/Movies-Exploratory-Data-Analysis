# Movies-Exploratory-Data-Analysis

# 🎬 Movies – Exploratory Data Analysis

## 📌 Projektbeschreibung

In diesem Projekt untersuche ich einen Datensatz mit Informationen zu Filmen.

Das Ziel ist, den Datensatz zunächst zu verstehen und zu bereinigen. Anschließend werden erste Zusammenhänge zwischen verschiedenen Eigenschaften von Filmen untersucht.

Dabei geht es zum Beispiel um folgende Fragen:

* Wie ist der Datensatz aufgebaut?
* Gibt es fehlende oder doppelte Werte?
* Wie hoch sind Budget, Umsatz und Gewinn?
* Welche Filmgenres kommen besonders häufig vor?
* Haben populärere Filme im Durchschnitt einen höheren Umsatz?

Das Projekt wurde mit **Python, Pandas, NumPy, Matplotlib und Seaborn** umgesetzt.

---

## 🎯 Ziel des Projekts

Das Hauptziel ist es, einen realen Datensatz mit Python systematisch zu untersuchen.

Dabei möchte ich den typischen Ablauf einer **Exploratory Data Analysis (EDA)** kennenlernen:

**Daten laden → Daten verstehen → Daten bereinigen → Daten verändern → Daten untersuchen → Ergebnisse visualisieren**

---

## 📂 Datensatz

Für die Analyse wird der Datensatz `tmdb-movies.csv` verwendet.

Der ursprüngliche Datensatz enthält **10.866 Filme und 21 Spalten**.

Unter anderem sind folgende Informationen enthalten:

* `budget` – Produktionsbudget
* `revenue` – Umsatz des Films
* `popularity` – Popularitätswert
* `genres` – Genre des Films
* `vote_count` – Anzahl der Bewertungen
* `vote_average` – durchschnittliche Bewertung
* `release_year` – Erscheinungsjahr

---

## 🔎 Vorgehensweise

### 1. Daten laden

Zuerst wird der Datensatz mit Pandas eingelesen:

```python
df = pd.read_csv("tmdb-movies.csv")
```

Anschließend werden die ersten Zeilen und grundlegende Informationen über den Datensatz betrachtet.

---

### 2. Datensatz verstehen

Mit Funktionen wie

```python
df.info()
df.shape
df.describe()
```

wird untersucht, wie groß der Datensatz ist und welche Arten von Daten enthalten sind.

Außerdem wird überprüft, wie viele unterschiedliche Werte die einzelnen Spalten enthalten.

---

### 3. Fehlende Werte untersuchen

Mit

```python
df.isna().sum()
```

wird geprüft, in welchen Spalten Werte fehlen.

Dabei zeigt sich beispielsweise, dass insbesondere bei `homepage`, `tagline` und `keywords` viele Werte fehlen.

Da diese Spalten für die weitere Analyse nicht benötigt werden, werden sie später entfernt.

---

### 4. Doppelte Daten entfernen

Anschließend wird geprüft, ob Filme doppelt im Datensatz vorhanden sind:

```python
df.duplicated().sum()
```

Es wurde **eine doppelte Zeile** gefunden und entfernt.

---

### 5. Neue Variable `profit` erstellen

Um den finanziellen Erfolg eines Films einfacher untersuchen zu können, wird eine neue Spalte erstellt:

```python
df["profit"] = df["revenue"] - df["budget"]
```

Der Gewinn wird also vereinfacht als

**Umsatz − Budget = Profit**

berechnet.

---

### 6. Nicht benötigte Spalten entfernen

Für die weitere Analyse werden nur die relevanten Informationen behalten.

Dadurch wird der Datensatz von ursprünglich **21 Spalten auf 8 Spalten** reduziert:

* `popularity`
* `budget`
* `revenue`
* `genres`
* `vote_count`
* `vote_average`
* `release_year`
* `profit`

Das macht die weitere Analyse übersichtlicher.

---

### 7. Fehlende Werte entfernen

Nach der Auswahl der relevanten Spalten gibt es noch fehlende Werte in der Spalte `genres`.

Diese werden entfernt:

```python
df.dropna(inplace=True)
```

Danach enthält der Datensatz **10.842 Filme**.

---

### 8. Genres vereinfachen

In der ursprünglichen Spalte `genres` können mehrere Genres für einen Film stehen, die mit `|` getrennt sind.

Beispiel:

```text
Action|Adventure|Science Fiction
```

Für diese erste Analyse wird jeweils nur das erste Genre verwendet.

---

### 9. Werte kategorisieren

Die durchschnittliche Filmbewertung wird mithilfe von Quartilen in vier Gruppen eingeteilt:

* `not_popular`
* `below_Average`
* `Average`
* `popular`

Auch der `profit` wird in drei Kategorien eingeteilt:

* `low`
* `average`
* `high`

Dafür wird die Pandas-Funktion `qcut()` verwendet.

---

## 📊 Erste Analyse

Eine der ersten untersuchten Fragen lautet:

> **Haben populärere Filme im Durchschnitt einen höheren Umsatz?**

Dafür wird der durchschnittliche Popularitätswert berechnet und die Filme in zwei Gruppen aufgeteilt:

* Filme mit einer Popularität unter bzw. gleich dem Durchschnitt
* Filme mit einer Popularität über dem Durchschnitt

Die durchschnittlichen Umsätze der beiden Gruppen werden anschließend miteinander verglichen.

Im Datensatz ergibt sich:

| Gruppe                       | Durchschnittlicher Umsatz |
| ---------------------------- | ------------------------: |
| Weniger populär              |              ca. 7,7 Mio. |
| Überdurchschnittlich populär |            ca. 122,0 Mio. |

In diesem Datensatz haben die Filme mit höherer Popularität damit einen deutlich höheren durchschnittlichen Umsatz.

**Wichtig:** Das zeigt zunächst einen Zusammenhang innerhalb dieses Datensatzes. Daraus lässt sich nicht automatisch schließen, dass eine höhere Popularität die Ursache für einen höheren Umsatz ist.

---

## 🎥 Analyse der Filmgenres

Zusätzlich wird untersucht, welche Genres besonders häufig vorkommen.

Mit

```python
df["genres"].value_counts()
```

wird gezählt, wie viele Filme zu den jeweiligen Genres gehören.

Das häufigste Genre im bereinigten Datensatz ist **Drama** mit 2.453 Filmen.

Die Verteilung der Genres wird anschließend mit einem Balkendiagramm visualisiert.

---

## 🛠️ Verwendete Technologien

* **Python**
* **Pandas** – Daten einlesen, bereinigen und analysieren
* **NumPy** – numerische Berechnungen
* **Matplotlib** – Visualisierung
* **Seaborn** – Datenvisualisierung

---

## 📁 Projektstruktur

```text
Movies-EDA/
│
├── Movies_EDA.ipynb
├── tmdb-movies.csv
└── README.md
```

---

## 🚀 Was ich dabei gelernt habe

Durch dieses Projekt übe ich den grundlegenden Ablauf einer Datenanalyse mit Python.

Besonders habe ich dabei mit folgenden Konzepten gearbeitet:

* CSV-Dateien mit Pandas einlesen
* DataFrames untersuchen
* fehlende Werte finden und entfernen
* doppelte Daten erkennen
* Spalten auswählen und entfernen
* neue Variablen berechnen
* Daten kategorisieren
* einfache statistische Kennzahlen berechnen
* Gruppen miteinander vergleichen
* Daten visualisieren

Das Projekt dient damit als praktische Übung für **Data Science und Exploratory Data Analysis mit Python**.
