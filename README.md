# Arduino Music Synthesizer: "Bella Ciao"

This project utilizes the Arduino’s ability to generate specific pulse-width modulation (PWM) frequencies to play the iconic **"Bella Ciao"** theme through a piezoelectric buzzer.

---

## 🎵 Song Identification: "Bella Ciao"
The note sequence in this firmware (starting with `Mi, La, Si, Do2, La`) identifies the melody as the Italian protest folk song **"Bella Ciao"**, which gained modern global recognition via the series *Money Heist*.

---

## 🏗️ System Overview
The firmware maps musical notes to physical frequencies (in Hz) and calculates rhythmic durations based on a **Beats Per Minute (BPM)** variable. This allows the Arduino to act as a basic square-wave synthesizer.

---

## 📐 Logic & Calculation Breakdown

### **1. Frequency Mapping**
Musical pitches are defined as integer variables representing Hertz (Hz):
*   **Low Octave**: Variables like `Do` (523 Hz) represent the middle-C range.
*   **High Octave**: Variables with a '2' suffix, like `Do2` (1046 Hz), represent the higher register.
*   The high octave values are exactly double the low octave, following the logarithmic nature of musical scales.

### **2. Rhythmic Scaling**
The `setup()` function translates the `bpm` into millisecond durations for different note types:
*   **Black (Quarter Note)**: Derived via `35000 / bpm`.
*   **White (Half Note)**: Twice the length of a black note.
*   **Rounda (Whole Note)**: Four times the length of a black note.
*   **Dotted Notes (`p` suffix)**: Calculated by multiplying the base note by **1.5**, following standard music theory.

### **3. The `tone()` Function**
The hardware execution relies on the `tone(pin, frequency, duration)` command:
*   **Frequency**: Vibrates the buzzer at the specific pitch.
*   **Duration**: Maintains the vibration for the calculated rhythmic length.
*   **Staccato Gap**: A `delay(duration + 50)` is used after each note to prevent notes from "bleeding" together, ensuring a crisp performance.

---

## 🔌 Hardware Wiring
| Pin | Function | Description |
| :--- | :--- | :--- |
| **DIGITAL 13** | Buzzer Output | Sends the square wave frequency to the piezo element. |
| **DIGITAL 12** | Buzzer Power | Acts as a secondary power trigger to enable the buzzer circuit. |

---

## 🚀 How to Use
1.  **Wiring**: Connect a Piezo Buzzer to DIGITAL 13 and a secondary power line (if required by your circuit) to DIGITAL 12.
2.  **BPM Adjustment**: Change the `int bpm = 120;` variable to speed up or slow down the song.
3.  **Upload**: Flash the code to your Arduino.
4.  **Listen**: The song will loop indefinitely, playing the "Bella Ciao" melody.

---
