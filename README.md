# Croatia: Best Sites for Solar and Wind Plants (Data Analysis)

A data pipeline that links **climate data** (sunshine hours and wind) with **CO₂ emissions** to rank Croatian locations by their potential for solar and wind power plants, and to estimate how much CO₂ those plants could avoid.

> Course project, Faculty of Organization and Informatics (FOI), University of Zagreb

## What it does

1. **Web scraping**: annual sunshine hours for 23 weather stations scraped from meteo.hr with `requests`, `pandas.read_html` and BeautifulSoup, with a local HTML cache.
2. **Wind estimate**: a wind speed is assigned per climate zone (inland, coast, island, mountain, high-wind), based on the national basic-wind-speed map documentation.
3. **CO₂ data**: the World Bank WDI CSV (transport CO₂ for Croatia, 1970–2024), with a fallback to the World Bank API.
4. **Scoring and ML**: MinMax-normalised solar, wind and combined scores, plus **K-Means** clustering of the locations.
5. **Impact estimate**: top-5 solar (50 MW) and top-5 wind (100 MW) sites with assumed capacity factors give about **0.82 Mt CO₂ avoided per year**, roughly **10 %** of Croatia's 2024 transport emissions.
6. **SQLite database** with `klima` and `ugljik` tables.
7. **Map**: GeoPandas map of Croatia with the high-potential sites.

**Top combined sites:** Zadar, Hvar, Mali Lošinj, Šibenik, Split.

## Tech stack

Python · pandas · NumPy · requests · BeautifulSoup · scikit-learn (K-Means, MinMaxScaler) · SQLite · GeoPandas · Matplotlib · Jupyter / Colab

## Run

Put the input files next to the notebook and run all cells:
- `API_EN.GHG.CO2.TR.MT.CE.AR5_DS2_en_csv_v2_174360.csv` ([World Bank WDI](https://data.worldbank.org/indicator/EN.GHG.CO2.TR.MT.CE.AR5))
- `obvY9201p50_detaljno.pdf` (basic wind speed map documentation)

> Note: the wind speeds per zone and the capacity factors are simplified assumptions, so the emission figure is an order-of-magnitude estimate and not an engineering result.

---

## Hrvatski

# Analiza podataka za smanjenje ugljičnog otiska RH: optimizacija lokacija za solarne i vjetroelektrane

Projektni zadatak u kojem se povezuju **klimatski pokazatelji** (osunčanost i vjetar) s **emisijama CO₂** kako bi se predložile lokacije u Hrvatskoj s najvećim potencijalom za obnovljive izvore.

### Postupak

- dohvat sunčanih sati za 23 postaje s meteo.hr (web scraping uz cache)
- procjena vjetra po klimatskim zonama
- emisije CO₂ iz WDI CSV-a, s pokušajem dohvata preko World Bank API-ja
- normalizacija, skorovi te K-Means klasteriranje lokacija
- procjena izbjegnutih emisija: oko 0,82 Mt CO₂ godišnje, što je oko 10 % emisija transporta u 2024.
- SQLite baza (`klima`, `ugljik`) i karta lokacija u GeoPandasu

Najbolje kombinirane lokacije su Zadar, Hvar, Mali Lošinj, Šibenik i Split.
