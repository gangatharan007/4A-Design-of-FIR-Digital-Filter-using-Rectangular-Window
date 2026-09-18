# FIR-FILTER-DESIGN
# EXP 4 A: Design-of-FIR-Digital-Filter-using-Rectangular-Window

# AIM 1:  To perform Design-of-LOWPASS FIR-Digital-Filter-using-Rectangular-Window using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```// Scilab code to generate the exact plots (Linear & dB Magnitude Response)
clear;
clc;
clf;

// 1. Filter Specifications
N = 7;                   // Filter length (7 taps)
wc = 0.2 * %pi;          // Cutoff frequency in radians (normalized to 0.2*pi)
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 3)

// 2. Impulse Response h(n) of ideal LPF with Rectangular Window
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = wc / %pi;
    else
        hd(i) = sin(wc * m) / (%pi * m);
    end
end

// Rectangular window w(n) = 1
w_rect = ones(1, N);
h = hd .* w_rect;

// 3. Frequency Response Calculation
w = linspace(0, %pi, 1000);  // Frequency vector from 0 to pi
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB (%eps prevents log(0))
norm_w = w / %pi;                     // Normalized Digital Frequency (0 to 1)

// 4. Plotting

// --- Subplot 1: Linear Magnitude Response ---
subplot(2, 1, 1);
plot(norm_w, mag, 'b', 'LineWidth', 1.5);
title('Frequency Response of FIR LPF using Rectangular Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
a1 = gca();
a1.data_bounds = [0, 0; 1, 1.2];
a1.x_ticks = tlist(["ticks", "locations", "labels"], 0:0.05:1, string(0:0.05:1));
a1.y_ticks = tlist(["ticks", "locations", "labels"], 0:0.2:1.2, string(0:0.2:1.2));

// --- Subplot 2: Decibel Magnitude Response ---
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b', 'LineWidth', 1.5);
title('Frequency Response of FIR LPF using Rectangular Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
a2 = gca();
a2.data_bounds = [0, -90; 1, 10];
a2.x_ticks = tlist(["ticks", "locations", "labels"], 0:0.05:1, string(0:0.05:1));
a2.y_ticks = tlist(["ticks", "locations", "labels"], -80:20:0, string(-80:20:0));
```

# OUTPUT: 
<img width="1536" height="704" alt="WhatsApp Image 2026-08-18 at 9 39 59 AM" src="https://github.com/user-attachments/assets/cf1a8276-b1be-45d5-87bf-dc4cfcbfdb3f" />


# RESULT: 

Thus design of low pass FIR digital filter using-Rectangular-Window waveforms were plotted and output was verified.

# AIM 2: To perform DESIGN OF HIGH PASS FIR DIGITAL FILTERS using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 

```
// Design of Highpass FIR Digital Filter using Rectangular Window
clear;
clc;
clf;

// 1. Filter Specifications
N = 7;                   // Filter length (odd)
wc = 0.5 * %pi;          // Cutoff frequency in radians (normalized to 0.5*pi)
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 3)

// 2. Impulse Response hd(n) for Ideal HPF
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = 1 - (wc / %pi);
    else
        hd(i) = -sin(wc * m) / (%pi * m);
    end
end

// 3. Apply Rectangular Window: w(n) = 1
w_rect = ones(1, N);
h = hd .* w_rect;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR HPF using Rectangular Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR HPF using Rectangular Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="1536" height="704" alt="image" src="https://github.com/user-attachments/assets/db802f96-158f-4f97-9c4a-fe0ebb6e2bfb" />


# RESULT: 
Thus design of HIGH pass FIR digital filter using-Rectangular-Window waveforms were plotted and output was verified.

# AIM 3: To perform DESIGN OF BAND PASS FIR DIGITAL FILTERS using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
// Design of Bandpass FIR Digital Filter using Rectangular Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc1 = 0.3 * %pi;         // Lower cutoff frequency
wc2 = 0.7 * %pi;         // Upper cutoff frequency
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal BPF
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = (wc2 - wc1) / %pi;
    else
        hd(i) = (sin(wc2 * m) - sin(wc1 * m)) / (%pi * m);
    end
end

// 3. Apply Rectangular Window: w(n) = 1
w_rect = ones(1, N);
h = hd .* w_rect;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BPF using Rectangular Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BPF using Rectangular Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="610" height="460" alt="image" src="https://github.com/user-attachments/assets/8bff0119-d5f6-492b-8787-23f3e64c4437" />


# RESULT: 
Thus design of BAND pass FIR digital filter using-Rectangular-Window waveforms were plotted and output was verified.

# AIM 4: To perform DESIGN OF BAND STOP FIR DIGITAL FILTER using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
// Design of Bandstop FIR Digital Filter using Rectangular Window
clear;
clc;
clf;

// 1. Simple Filter Specifications
N = 11;                  // Filter length (odd)
wc1 = 0.3 * %pi;         // Lower cutoff frequency (stopband start)
wc2 = 0.7 * %pi;         // Upper cutoff frequency (stopband end)
alpha = (N - 1) / 2;     // Center of symmetry (alpha = 5)

// 2. Impulse Response hd(n) for Ideal Bandstop Filter (BSF)
n = 0:(N - 1);
hd = zeros(1, N);

for i = 1:N
    m = n(i) - alpha;
    if m == 0 then
        hd(i) = 1 - ((wc2 - wc1) / %pi);
    else
        hd(i) = (sin(wc1 * m) - sin(wc2 * m)) / (%pi * m);
    end
end

// 3. Apply Rectangular Window: w(n) = 1
w_rect = ones(1, N);
h = hd .* w_rect;

// 4. Frequency Response (DTFT)
w = linspace(0, %pi, 1000);
H = zeros(1, length(w));

for k = 1:length(w)
    H(k) = sum(h .* exp(-%i * w(k) * n));
end

mag = abs(H);                         // Linear Magnitude
mag_dB = 20 * log10(mag + %eps);      // Magnitude in dB
norm_w = w / %pi;                     // Normalized frequency (0 to 1)

// 5. Plotting

// Subplot 1: Linear Magnitude Response
subplot(2, 1, 1);
plot(norm_w, mag, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BSF using Rectangular Window (Linear)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude', 'fontsize', 2);
xgrid(1);

// Subplot 2: Decibel (dB) Magnitude Response
subplot(2, 1, 2);
plot(norm_w, mag_dB, 'b-', 'LineWidth', 1.5);
title('Frequency Response of FIR BSF using Rectangular Window (dB)', 'fontsize', 3);
xlabel('Normalized Digital Frequency w', 'fontsize', 2);
ylabel('Magnitude in dB', 'fontsize', 2);
xgrid(1);
```

# OUTPUT: 
<img width="1536" height="704" alt="image" src="https://github.com/user-attachments/assets/15252a20-05e5-4753-b3dc-73c14bd98e34" />


# RESULT: 
Thus design of BAND STOP FIR digital filter using-Rectangular-Window waveforms were plotted and output was verified.
