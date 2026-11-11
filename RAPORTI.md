# Raporti i studentit: UrbanBike AI

Studenti: **[Plotëso emrin]**
Grupi (nëse punohet në grup): **[Plotëso]**
Data: **[Plotëso]**
GitHub-i im: **[Vendos linkun personal]**
Figma: **[Vendos linkun personal]**

## Qëllimi

Problemi që zgjidhim: Parashikimi i numrit të qirave të biçikletave për ditën pasuese në Washington, D.C., mbi të dhëna historike 2011–2012.

Target-i y: `rentals`, i marrë nga kolona `cnt` e datasetit UCI.

Predictorët X: `rentals_lag1`, `rentals_lag7`, `rentals_mean7`, `temp_c_lag7`, `rain_mm_lag7`, `wind_ms_lag7`, `trend_days`, `weekday`, `month`, `workingday`, `holiday`.

Koha kur parashikojmë dhe çfarë informacioni është i njohur: demonstrim historik një ditë përpara; supozojmë se qiratë e ditës së mëparshme janë të disponueshme, ndërsa moti merret nga 7 ditë më parë. Nuk përdoret vlera reale e target-it të ditës që parashikohet.

## Pastrimi

Burimet reale dhe çelësi i bashkimit: UCI `data/raw/day.csv` dhe NASA `data/raw/nasa_weather.csv`, bashkuar sipas datës.

Dallimi mes origjinaleve dhe kopjes didaktike: burimet ruhen të pandryshuara; kodi krijon një kopje me dublime, mungesa dhe probleme të tipeve për ushtrimin e pastrimit.

Rreshtat para/pas: 731 në burimin e bashkuar; 743 në kopjen didaktike para pastrimit; 731 pas pastrimit; 724 pas ndërtimit të predictorëve kohorë.

Dublimet: 12 dublime ekzakte të futura në kopjen didaktike.

Mungesat para/pas konvertimit: 30 qeliza bosh të raportuara para konvertimit; pas pastrimit mbeten 36 mungesa meteorologjike për trajtim në pipeline.

Arsyeja e imputimit vetëm me train: për të shmangur rrjedhjen e informacionit nga validation dhe test në parametrat e përpunimit.

## Grafikët

Vëzhgimi 1 dhe figura përkatëse: `reports/figures/02_workingday.png`. Në train, mesatarja e qirave është rreth 3761 në ditë pune dhe 3570 në ditë jo pune.

Vëzhgimi 2 dhe figura përkatëse: `reports/figures/03_weather.png`. Në train, korrelacioni i temperaturës së të njëjtës ditë me qiratë është rreth 0.58; ky është vëzhgim eksplorues, jo predictor i përdorur nga modeli për atë ditë.

Pse një lidhje e dukshme nuk provon shkakësi: mund të ndikojnë sezonaliteti, kalendari dhe faktorë të tjerë të pamatur.

## Vlerësimi

Ndarja kohore: train 479 ditë (2011-01-08 deri 2012-04-30); validation 123 ditë (2012-05-01 deri 2012-08-31); test 122 ditë (2012-09-01 deri 2012-12-31).

| Modeli | Validation MAE | Test MAE | Test RMSE | Test R² |
|---|---:|---:|---:|---:|
| Yesterday | 775.20 | 916.40 | 1330.39 | 0.539 |
| DummyMean | 2953.87 | 2494.63 | 2790.06 | -1.027 |
| Ridge | 687.56 | 893.25 | 1252.65 | 0.591 |
| RandomForest | 1821.53 | 1671.50 | 2042.65 | -0.087 |

Modeli i zgjedhur nga validation dhe arsyeja: **Ridge**, me MAE më të ulët në validation (687.56).

Rezultati i provës me Random Forest: MAE në validation 1821.53, më i lartë se Ridge.

Interpretimi i gabimit në qira për ditë: MAE e Ridge në test (893.25) do të thotë se gabimi absolut mesatar është rreth 893 qira për ditë.

Rezultati i klasifikimit: pragu i medianës së train është 3907 qira; Logistic Regression arrin accuracy 0.918, balanced accuracy 0.780 dhe macro-F1 0.820 në test.

## Kufizimet

1. Dataseti përmban vetëm vitet 2011–2012 në Washington, D.C.; nuk vërteton performancë aktuale.
2. Parashikimi mbështetet në qiratë e djeshme dhe në motin e 7 ditëve më parë, jo në një parashikim meteorologjik të drejtpërdrejtë.
3. Rezultatet e testit varen nga kjo ndarje kohore dhe nuk garantojnë përgjithësim në periudha të tjera.

## Kontributet individuale

| Studenti | Skedari/ekrani | Puna dhe vendimi | Commit/prova |
|---|---|---|---|
| [Emri] | [Skedari/Figma] | [Përshkruaj kontributin real] | [Commit/link] |

## Burimet

UCI: https://doi.org/10.24432/C5W894

NASA: https://power.larc.nasa.gov/docs/services/api/temporal/daily/

Provenienca lokale: `data/raw/provenance.json`
