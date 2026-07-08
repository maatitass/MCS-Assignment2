# Progetto 2 - Metodi del Calcolo Scientifico

**Autori:**
- Matias Bonoli (matricola 912941)
- Ashley Chudory (matricola 935003)
- Daniele Maccagnan (matricola 945269)

Compressione di immagini in scala di grigio con DCT.

Implementazione Python di quanto richiesto dal progetto:

- DCT2 fatta in casa
- DCT2 fast tramite `scipy.fft`
- Compressione di immagini tramite taglio delle frequenze
- GUI minimale

## Dipendenze

```bash
python -m pip install -r requirements.txt
```

## Esecuzione completa

Dalla cartella del progetto:

```bash
python src/run_assignment.py
```

Questo comando esegue i benchmark su varie dimensioni di matrici (da 8 a 1024) e 
applica la compressione su tutte le immagini `.bmp` presenti nella cartella `immagini`
per diverse combinazioni di blocchi `F` e soglie di taglio `d`.

Gli output vengono salvati in:

- `results/benchmark.csv`
- `results/benchmark_dct2.png`
- `results/examples/` (griglie, metriche in csv e grafici)

## Esecuzione su parametri specifici

```bash
python src/run_assignment.py --size 32
```

Si possono indicare piu' dimensioni o immagini ripetendo gli argomenti:

```bash
python src/run_assignment.py --size 16 --size 32 --image immagini/320x320.bmp
```

Per eseguire solo il benchmark saltando le immagini:

```bash
python src/run_assignment.py --no-examples
```

## Interfaccia grafica (GUI)

```bash
python src/gui.py
```

La GUI permette di selezionare visivamente un'immagine, scegliere i parametri `F` e `d`,
e visualizzare in tempo reale l'originale a confronto con l'immagine compressa.

## Test veloci

```bash
python src/test_assignment.py
```

I test controllano i due blocchi numerici del PDF fornito, la coerenza tra DCT2 fatta
in casa e DCT2 fast, l'inversa IDCT2 e la corretta applicazione della maschera di taglio.
