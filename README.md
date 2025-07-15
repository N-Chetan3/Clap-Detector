# Clap Detection Using Energy-Based Analysis

This project detects sharp sounds such as **hand claps** from an audio file using **short-time energy (STE)** and **peak detection**. The implementation is done in **Python** using **Librosa**, **Matplotlib**, and **Scipy**, and designed to run in **Google Colab**.

---

##  Logic & Algorithm

1. **Short-Time Energy (STE)**:
   - The audio is divided into overlapping short frames.
   - Energy is calculated for each frame using the **sum of squared amplitudes**.
   - This highlights sudden bursts of sound energy.

2. **Normalization**:
   - The energy values are normalized between 0 and 1 so that a fixed threshold like `0.5` becomes meaningful across various audio levels.

3. **Fixed Thresholding**:
   - A constant threshold value (`0.5`) is applied to the normalized energy.
   - Frames with energy values exceeding this threshold are considered potential clap or keyword events.
   - Threshold can be adjusted for various scenarios.

4. **Peak Detection**:
   - `scipy.signal.find_peaks` is used to detect **local maxima** (peaks) in the energy signal that cross the threshold.
   - Detected peak indices are converted to **timestamps**.

---

## 🧩 Function & Module Descriptions

| Function / Module               | Purpose |
|--------------------------------|---------|
| `librosa.load()`               | Loads audio and returns waveform (`y`) and sample rate (`sr`). |
| `np.sum(...**2)`               | Computes short-time energy per frame (squared sum of samples). |
| `np.max()`                     | Used to normalize the energy values. |
| `find_peaks()`                 | Identifies high-energy peaks in the normalized energy signal. |
| `librosa.frames_to_time()`     | Converts frame indices to actual time (seconds). |
| `librosa.display.waveshow()`   | Plots the waveform of the audio. |
| `matplotlib.pyplot`            | Used for plotting waveform, energy, and detected peaks. |
| `Audio()`                      | Allows playback of uploaded audio. |
| `files.upload()`               | Google Colab widget to upload audio files interactively. |

---

## 📊 Visual Outputs

The notebook produces 3 useful plots:

1. **Audio Waveform** with vertical red lines marking detected events.
2. **Raw Short-Time Energy** with red 'X' marks at peaks.
3. **Normalized Energy Curve** with:
   - Red '🔴' marks for peaks
   - A horizontal line at `y = 0.5` to show the detection threshold

---

##  Example Output

For the 6-second sample audio with 3 hand claps:

```text
Threshold: 0.5
Detected peak timestamps (in seconds):
• 2.02 s
• 3.38 s
• 5.03 s
