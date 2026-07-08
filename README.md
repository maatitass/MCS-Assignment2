# Assignment 2 - Compressione immagini tramite DCT

Progetto Python semplice per il secondo assignment di Metodi del Calcolo
Scientifico. Il codice implementa:

- DCT2 fatta in casa con matrice ortonormale esplicita, come nei file MATLAB del professore;
- DCT2 fast tramite `scipy.fft`;
- compressione di immagini BMP in scala di grigi tramite taglio delle frequenze;
- GUI minimale per scegliere immagine, `F` e `d`.

La relazione si trova in `relazione/relazione.pdf`; questo README e' operativo.

## Dipendenze

Usare un ambiente locale, senza installazioni globali:

```bash
uv venv
uv pip install -r requirements.txt
```

## Test

```bash
uv run python src/test_assignment.py
```

I test controllano i due blocchi numerici del PDF, il confronto tra DCT2 fatta
in casa e DCT2 fast, la IDCT2, la maschera `k + ell >= d` e la compressione di
una piccola immagine.

## Benchmark ed esempi

```bash
uv run python src/run_assignment.py
```

Output principali:

- `results/benchmark.csv`
- `results/benchmark_dct2.png`
- `results/examples/*_grid.png`
- `results/examples/*_metrics_plot.png`
- `results/examples/*_metrics.csv`

Il benchmark standard usa:

```text
N = 8, 16, 32, 64, 128, 256, 512, 768, 1024
```

Per usare dimensioni specifiche nel benchmark:

```bash
uv run python src/run_assignment.py --size 16 --size 32 --size 64
```

Per generare gli esempi solo per una immagine specifica:

```bash
uv run python src/run_assignment.py --image immagini/320x320.bmp
```

Per ogni immagine vengono provate 12 coppie `(F, d)` fisse: quattro con
`F = 8`, quattro con `F = 16` e quattro con `F = 32`.

Il parametro `F` e' la dimensione dei blocchi quadrati. Il parametro `d` deve
rispettare:

```text
0 <= d <= 2F - 2
```

I coefficienti eliminati sono quelli con indice `k + ell >= d`, usando indici
che partono da zero.

## GUI

```bash
uv run python src/gui.py
```

La GUI permette di scegliere un file `.bmp`, inserire `F` e `d`, e vedere
subito l'immagine originale selezionata con la sua dimensione. Dopo aver
premuto `Comprimi`, mostra affiancate l'immagine originale intera e quella
ricostruita sui blocchi completi usati dalla DCT2. Le due anteprime vengono
ridimensionate dentro la finestra senza tagliare l'immagine.

Sotto le caselle `F` e `d` la GUI mostra anche i valori ammessi:

- sotto `F`, dato `d`, indica il minimo `F` necessario;
- sotto `d`, dato `F`, indica il range valido per `d`;
- se un'immagine e' selezionata, indica anche il massimo `F` possibile per
  avere almeno un blocco completo.

Se `F` non divide esattamente larghezza o altezza, il risultato compresso usa
solo la parte dell'immagine coperta da blocchi completi, come richiesto dal
testo del progetto. La GUI lascia comunque visibile l'immagine originale intera
a sinistra e indica in basso la dimensione effettivamente usata per la DCT2.

## Struttura

- `src/dct_utils.py`: funzioni DCT, IDCT, maschera frequenze e compressione;
- `src/run_assignment.py`: benchmark DCT2 e generazione esempi;
- `src/gui.py`: interfaccia Tkinter minimale;
- `src/test_assignment.py`: test veloci senza framework esterni;
- `immagini/`: immagini BMP fornite dal docente.
