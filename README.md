# Analiza koszyka: reguły asocjacyjne (EconoShop Express)

Eksploracja danych, laboratorium 6. Dane syntetyczne: 7 968 paragonów sklepu osiedlowego z września i października 2026 r. (`dane/paragony.csv`, jeden wiersz = jeden produkt na paragonie).

| Plik | Co to jest |
|---|---|
| `koszyk.py` | funkcje: macierz koszyków, wsparcie, pewność, lift, Apriori, scenariusz zysku (TODO 1–3 do uzupełnienia) |
| `tests/test_koszyk.py` | testy (`pytest -q`); na start `7 failed`, po TODO 1–3 `7 passed` |
| `lab6_student.ipynb` | notatnik z zadaniami Z1–Z6 |
| `app.py` | dashboard Streamlit |
| `render.yaml` | wdrożenie na Render |
| `.devcontainer/` | konfiguracja GitHub Codespaces (Python 3.13 i biblioteki instalują się same) |
| `.github/workflows/testy.yml` | testy na GitHubie po każdym push |

## 1. Praca w GitHub Codespaces

1. **Code → Codespaces → Create codespace on main**; poczekaj na koniec instalacji.
2. W terminalu: `pytest -q`, uzupełnij TODO 1–3 w `koszyk.py`, aż zobaczysz `7 passed`.
3. Otwórz `lab6_student.ipynb` → **Select Kernel → Python 3.13** → uruchamiaj komórki po kolei (Shift + Enter).
4. `streamlit run app.py` → **Open in Browser** (albo zakładka PORTS → 8501).

## 2. Zapis zmian

Panel **Source Control** → opis → **Commit** → **Sync Changes** (albo `git add .`, `git commit -m "..."`, `git push`). Zakładka **Actions**: zielony znaczek = testy przechodzą.

## 3. Render

**New → Blueprint** → **Connect** przy tym repozytorium → **Deploy Blueprint**. Ręcznie: **New → Web Service**, Build `pip install -r requirements.txt`, Start `streamlit run app.py --server.port $PORT --server.address 0.0.0.0 --server.headless true`, zmienna `PYTHON_VERSION` = `3.13.5`. Usługa Free usypia po 15 min bez ruchu.

## 4. Rekomendacja dla kierownika sklepu

Makaron → sos pomidorowy: 207 paragonów, pewność 0,312, lift 5,97; ustawiamy sos obok makaronu bez rabatu, bo 207 z 664 klientów z makaronem i tak kupuje oba. Rabat 20% na sos dałby przy naszych założeniach (marża 2,10 zł, konwersja 5%) wynik −273,80 zł i zwróciłby się dopiero przy konwersji 90,6%, a sama ekspozycja daje około +47,99 zł w dwa miesiące. Pieluchy → chusteczki nawilżane: 108 paragonów, pewność 0,307, lift 6,33; proponujemy zestaw (chusteczki w ofercie „razem z pieluchami” przy tej samej półce). Nie polecamy reguły pieluchy → piwo jako ustawienia na cały dzień: lift 1,54 w całych danych, ale 2,95 w godzinach 17–19 i 0,97 poza nimi, więc to związek zależny od pory dnia, który średnia ukrywa. Test A/B: ekspozycja i zestaw w połowie sklepów przez 4 tygodnie, druga połowa bez zmian; mierzymy odsetek paragonów z makaronem, na których jest sos (bazowo 31,2%), i paragonów z pieluchami, na których są chusteczki (bazowo 30,7%). Adres aplikacji: https://TUTAJ-WKLEJ-ADRES.onrender.com
