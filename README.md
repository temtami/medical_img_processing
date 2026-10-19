# Biomedical Signal Processing: ECG, EEG, EMG and EOG

This repository contains Jupyter notebooks for exploring and analyzing four types of biomedical signals:

- **ECG (Electrocardiogram):** electrical activity of the heart
- **EEG (Electroencephalogram):** electrical activity of the brain, organized here into frequency bands
- **EMG (Electromyogram):** electrical activity produced by skeletal muscles
- **EOG (Electrooculogram):** electrical potential associated with eye movements

The notebooks use Python to load signal data, visualize waveforms, perform basic preprocessing, and calculate selected signal characteristics.

## Repository Contents

| File | Purpose |
|---|---|
| `ECG(1).ipynb` | ECG visualization, resampling, band-pass filtering, R-peak detection, heart-rate estimation, smoothing, and an SNR calculation |
| `EEG.ipynb` | Loading Alpha, Beta, Delta, and Theta signals; resampling; plotting band signals; estimating SNR, power spectral density (PSD), and band power |
| `EMG(1).ipynb` | EMG resampling, band-pass filtering, rectification, envelope extraction, and an SNR-analysis section |
| `EOG.ipynb` | EOG baseline removal, smoothing, eye-movement peak detection, SNR estimation, and PSD visualization |

## Requirements

Use Python 3 with the following libraries:

- `numpy`
- `pandas`
- `matplotlib`
- `scipy`
- Jupyter Notebook or Google Colab

Install the required libraries locally with:

```bash
pip install numpy pandas matplotlib scipy jupyter
```

## Input Data

The notebooks expect CSV files with signal data. The filenames currently referenced in the code are:

### ECG
- `Default Dataset.csv`

The code reads the first column as time and the second column as ECG amplitude.

### EEG
- `EEG(alpha).csv`
- `EEG(beta).csv`
- `EEG(delta).csv`
- `EEG(theta).csv`

The code reads the second column from each file as the corresponding EEG band signal. The notebook maps the bands as Alpha (8–13 Hz), Beta (13–30 Hz), Delta (0.5–4 Hz), and Theta (4–8 Hz).

### EMG
- `EMG2.csv`

The code reads the first column as time and the second column as EMG amplitude.

### EOG
- `EOG.csv`

The code reads the first column as time and the second column as EOG amplitude.

**Important:** Place the required CSV files in the notebook's working directory, or update the paths in the notebooks. If running in Google Colab, upload the relevant CSV files when prompted. The CSV files are inputs and are not included with these notebooks unless separately added to the repository.

## How to Run

### Option 1: Google Colab

1. Upload the notebook to Google Colab.
2. Upload the CSV file or files required by that notebook when prompted.
3. Run the cells from top to bottom.
4. Review the generated plots and printed measurements.

### Option 2: Run locally

1. Clone or download this repository.
2. Install the dependencies listed above.
3. Put the required CSV files in the working directory.
4. Start Jupyter:

   ```bash
   jupyter notebook
   ```

5. Open the notebook you want to run and execute its cells in order.

## Analysis Workflow

### ECG
1. Load and plot the ECG waveform.
2. Resample the signal to a uniform time axis (the notebook assumes 250 Hz).
3. Apply a 0.5–40 Hz Butterworth band-pass filter.
4. Detect candidate R-peaks.
5. Estimate heart rate from R–R intervals and smooth the resulting series.
6. Calculate an SNR estimate.

### EEG
1. Load the Alpha, Beta, Delta, and Theta CSV files.
2. Resample the signals to a common 60-second time axis.
3. Plot each band.
4. Estimate band-specific SNR.
5. Compare power spectral density and calculate mean-square band power.

### EMG
1. Load and plot the EMG data.
2. Resample using an assumed 1000 Hz sampling frequency.
3. Apply a 20–450 Hz Butterworth band-pass filter.
4. Rectify the filtered signal and calculate a moving-average envelope.
5. Plot the filtered signal and envelope.
6. The final SNR section includes references to additional variables that may need to be defined before it can run independently; see Notes and Limitations.

### EOG
1. Load the EOG waveform and estimate its sampling frequency from the time column.
2. Remove the mean baseline and smooth the signal.
3. Detect candidate eye-movement peaks.
4. Estimate SNR using a 0.1–10 Hz frequency band.
5. Plot the power spectral density.

## Notes and Limitations

- These notebooks are exploratory signal-processing examples, not validated clinical tools.
- Sampling frequencies and time durations are assumed in some cells. Confirm them against the source data before interpreting results.
- Filtering bands and peak-detection thresholds may need adjustment for different datasets.
- The ECG notebook's final SNR cell refers to `time_common` and `ecg_r`, which are not defined earlier in that notebook as currently written.
- The EMG notebook's final SNR cell refers to variables and a resampling function (including `emg_r`, `ecg_r`, `ecg_sig`, `emg_sig`, `time_ecg`, `time_emg`, and `resample`) that are not all defined in that notebook. That section may need to be adapted or removed to run independently.
- Check the CSV column order, units, missing values, and time range before running the analysis.
- SNR values depend on the chosen frequency band and the definition of signal versus noise power. They should be interpreted as estimates under the notebook's current assumptions.

## Disclaimer

This repository is intended for educational and research use in signal processing. It is not intended for diagnosis, treatment, or other clinical decision-making.

## License

Add a license file if you intend to distribute or reuse this project publicly. Until a license is specified, reuse permissions are not explicitly granted.
