# UrbanBike AI — Udhëzime ekzekutimi

Ky projekt është ndërtuar duke bashkuar **kodin e prezantimit të pedagogut** (pjesët e slajdeve) me **datasetet e ZIP-it fillestar**. Skedari `RAPORTI.md` ka një draft të plotësuar me rezultate të verifikuara; plotëso vetë emrin, grupin, kontributin, GitHub dhe Figma.

## Windows (VS Code / PowerShell)

1. Instalo Python 3.12, Git dhe VS Code. Në VS Code instalo Python, Python Debugger dhe Pylance.
2. Hap `File > Open Folder` dhe zgjidh `urbanbike-ai-student`.
3. Hap `Terminal > New Terminal` dhe ekzekuto:

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pip check
.\.venv\Scripts\python.exe run_all.py
.\.venv\Scripts\python.exe app.py
```

4. Hap `http://127.0.0.1:8000` në shfletues. Zgjidh një datë nga periudha e testit dhe kliko **Parashiko**.
5. Ndale serverin me `Ctrl+C`.

## macOS / Linux

Me Python 3.12 të instaluar:

```bash
python3.12 -m venv .venv
./.venv/bin/python -m pip install -r requirements.txt
./.venv/bin/python -m pip check
./.venv/bin/python run_all.py
./.venv/bin/python app.py
```

Hap `http://127.0.0.1:8000`. Në VS Code zgjidh `Python: Select Interpreter` dhe `.venv`.

## Struktura dhe funksionet

- `data/raw/` — të dhënat origjinale UCI dhe NASA, të paprekura
- `config/common.py` — rrugët, predictorët, pipeline dhe ndarjet kohore
- `01_clean.py` — bashkimi, pastrimi dhe krijimi i variablave kohorë
- `02_visualize.py` — tre grafikë eksplorues
- `03_train.py` — Yesterday, DummyMean, Ridge, RandomForest dhe krahasimi
- `04_classify.py` — klasifikimi i kërkesës me LogisticRegression
- `run_all.py` — ekzekuton të katër fazat në rend
- `app.py` — server lokal HTTP, ndërfaqe dhe API `/api/predict?date=2012-09-01`
- `reports/` — metrikat, tabelat, figurat dhe auditimi
- `models/` — modelet e trajnuara (nuk përfshihen në Git sipas `.gitignore`)
- `RAPORTI.md` — raporti i laboratorit, me fushat personale për t'u plotësuar

## GitHub

Pasi të kesh konfiguruar emrin dhe email-in tënd:

```bash
git init
git config user.name "Emri Mbiemri"
git config user.email "emaili-yt@example.com"
git add .
git commit -m "UrbanBike AI - projekti i laboratorit"
```

Në VS Code përdor `Source Control > Publish Branch` dhe hyr në llogarinë tënde GitHub. Mos e publikoni me emrin e një personi tjetër. Shto URL-në reale në `RAPORTI.md` dhe bëj commit/push të ndryshimit.

## Figma

Krijo një skedar `UrbanBike AI – Emri Mbiemri` në https://figma.new me frame 1440×900. Vendos titullin, fushën e datës, butonin `Parashiko` dhe seksionin e rezultateve: qiratë e parashikuara, vlera reale, gabimi absolut. Vendos lidhjen e skedarit tënd në `RAPORTI.md`. Figma është koncept vizual, jo aplikacioni që kryen parashikimin.

## Shënim për rezultatet

Rezultatet janë llogaritur mbi të dhëna historike 2011–2012. Aplikacioni pranon vetëm datat e ndarjes test (2012-09-01 deri 2012-12-31); nuk ofron parashikime për data të sotme.
