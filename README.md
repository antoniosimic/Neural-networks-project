# Neural networks project – Tim 06

Projekt iz kolegija **Neuronske mreže**: automatska procjena stupnja **dijabetičke retinopatije (DR)** iz fundus snimki mrežnice.

**Tim:** Antonio Šimić (voditelj), Jakov Malić, Josip Gregorić, Andrej Pavić

## Skup podataka

[APTOS 2019 Blindness Detection (Kaggle)](https://www.kaggle.com/competitions/aptos2019-blindness-detection/data)

- 3662 označene slike (`train.csv`), 1928 neoznačenih (`test.csv`), ~8.6 GB
- 5 klasa (`diagnosis`): 0 – No DR, 1 – Mild, 2 – Moderate, 3 – Severe, 4 – Proliferative DR
- Izražen disbalans klasa (No DR 49.3 % naspram Severe 5.3 %, omjer ≈ 9.4)

Podaci nisu dio repozitorija – preuzimaju se s Kagglea (potreban `~/.kaggle/kaggle.json` i prihvaćena pravila natjecanja).

## Napredak

| Termin | Tema | Predano |
|---|---|---|
| 2. | Podaci i literatura – analiza skupa podataka | [`izvjestaji/06_izvjestaj_1.pdf`](izvjestaji/06_izvjestaj_1.pdf) |

### Ključni nalazi analize (2. termin)

- **Shortcut learning rizik:** rezolucija snimke snažno korelira s oznakom (npr. 92.5 % slika 1050×1050 je No DR) – model bi mogao učiti uređaj, a ne bolest.
- **Duplikati:** 143 grupe identičnih snimki (295 slika), od toga 38 grupa s **konfliktnim oznakama** → šum u oznakama.
- **Podjela train/val/test (70/15/15):** stratificirano po klasi i grupirano po duplikatima (bez curenja između skupova).
- **Predobrada:** obrezivanje crnih rubova, Histogram Equalization, CLAHE, Ben Graham metoda.
- Težine klasa za funkciju gubitka radi ublažavanja disbalansa.

## Pokretanje

```bash
pip install numpy pandas matplotlib seaborn opencv-python-headless pillow imagehash tqdm scikit-learn kaggle nbconvert
kaggle competitions download -c aptos2019-blindness-detection -p data
unzip -q data/aptos2019-blindness-detection.zip -d data
jupyter notebook 06_kod_1.ipynb
```
