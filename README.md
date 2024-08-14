# EE338 - Filter Design Assignment Report

**Harshraj Chaudhari, 210040060**  
**August 14, 2024**

## 1. Overview of the Assignment

### 1.1 Aim
- To design a Multi-Band Pass Filter, with pass-bands from two given frequency groups according to the filter specifications assigned.

### 1.2 Un-normalized Discrete Time Filter
- **Filter Number assigned**: M = 15
  - Since M = 11 ∗ Q + R, Q = 1 and R = 4
- **Passbands**: (40 + 5D) to (70 + 5D) and (170 + 5D) to (200 + 5D)
  - Group I Frequency Passband: D = Q = 1 ⇒ 45 − 75 kHz
  - Group II Frequency Passband: D = R = 3 ⇒ 190 − 220 kHz

**Filter Specifications**:
- FIR filter - designed using Kaiser Window
- Passbands: 45 kHz to 75 kHz and 190 kHz to 220 kHz
- Transition Bands: 5 kHz on either side of passband
- Stopbands: 0 − 40 kHz, 80 − 185 kHz, and 225 − 300 kHz (Sampling rate is 600 kHz)
- Tolerance: 0.15 in magnitude for both Passband and Stopband

### 1.3 Design Approach
The approach here is to design a Bandpass and a Bandstop Filter, such that their cascade gives us the desired filter. For the window, we are going to use a Kaiser Window. The filter length is obtained from the Kaiser window. The Kaiser window, denoted by \( w_K(n) \), is defined as:

\[ w_K(n) = \begin{cases} 
\frac{I_0 \left( \beta \sqrt{1 - \left( \frac{n}{N-1} \right)^2} \right)}{I_0(\beta)}, & \text{if } 0 \leq |n| \leq N - 1 \\
0, & \text{otherwise}
\end{cases} \]

where \( I_0(\cdot) \) is the modified Bessel function of order zero, \( N \) is the length of the window, \( n \) is the sample index, and \( \beta \) is a parameter that controls the shape of the window.

The filter length \( N \) in the Kaiser window method can be determined based on the desired specifications of the FIR filter, such as the transition bandwidth, passband ripple, and stopband attenuation. A common approach is to use the formula proposed by Kaiser:

\[ N = \frac{A_s - 8}{2.285 \Delta \omega} \]

where \( A_s \) is the desired stopband attenuation in decibels, and \( \Delta \omega \) is the transition bandwidth normalized to the Nyquist frequency.

The parameter \( \beta \) in the Kaiser window function is typically calculated based on the desired stopband attenuation \( A_s \). One common formula for calculating \( \beta \) is given by:

\[ \alpha = \begin{cases} 
0, & \text{for } A_s \leq 21 \\
0.5842(A_s - 21)^{0.4} + 0.07886(A_s - 21), & \text{for } 21 < A_s < 50 \\
0.1102(A_s - 8.7), & \text{for } A_s \geq 50
\end{cases} \]

\[ \beta = \alpha N \]

### 1.4 Normalized Discrete Time Filter
The sampling frequency is 600 kHz. Using this, we can work out the discrete filter specification. The specifications are as follows:

\[ \omega_n = \omega \times \frac{2\pi}{\omega_s} \quad (\omega_s = 600 \text{ kHz}) \]

**Normalized discrete filter specifications**:
- Passbands: \( \frac{3\pi}{20} \) to \( \frac{\pi}{4} \) and \( \frac{19\pi}{30} \) to \( \frac{11\pi}{15} \)
- Transition Bands: 0.016π on either side of passband
- Stopbands: \( 0 - \frac{2\pi}{15} \), \( \frac{4\pi}{15} - \frac{37\pi}{60} \), and \( \frac{3\pi}{4} - \pi \)
- Tolerance: 0.15 in magnitude for both Passband and Stopband

## 2. Band Pass Design

### 2.1 Un-normalized Discrete Time Filter Specifications
- FIR filter - designed using Kaiser Window
- Passband: 45 kHz to 220 kHz
- Transition Bands: 5 kHz on either side of passband
- Stopbands: 0 − 40 kHz and 225 − 300 kHz
- Tolerance: 0.15 in magnitude for both Passband and Stopband

### 2.2 Normalized Discrete Filter Specifications
- Passbands: \( \frac{3\pi}{20} \) to \( \frac{11\pi}{15} \)
- Transition Bands: 0.016π on either side of passband
- Stopbands: \( 0 - \frac{2\pi}{15} \), and \( \frac{3\pi}{4} - \pi \)
- Tolerance: 0.15 in magnitude for both Passband and Stopband

### 2.3 Band-pass Filter using Kaiser Window
**Bandpass Characteristics**:

| Data  | Value   |
|-------|---------|
| ∆ω1   | 0.0523  |
| ∆ω2   | 0.0523  |
| N     | 41.0    |
| A     | 16.478  |
| α     | 0       |
| ωc1   | 0.4450  |
| ωc2   | 2.3300  |
| β     | 0.0     |

The ideal band-pass filter and consequent calculation are given by:

\[ h_{\text{ideal}} = \frac{\sin(\omega_{c2}k) - \sin(\omega_{c1}k)}{\pi k} \quad \text{for } k \in \{-N, -N + 1, \ldots, N - 1, N\} \]

\[ h_{\text{kaiser}} = w_K(2N + 1) \]

\[ h_{\text{bp}} = h_{\text{ideal}} \cdot h_{\text{kaiser}} \]

![Bandpass Filter](bandpass_filter.png)
*Figure 1: (a) Filter Coefficients (b) Frequency Response*

## 3. Band Reject Filter

### 3.1 Un-normalized Discrete Time Filter Specifications
- FIR filter - designed using Kaiser Window
- Passband: 0 − 75 kHz and 190 − 300 kHz
- Transition Bands: 5 kHz on either side of passband
- Stopband: 80 − 185 kHz
- Tolerance: 0.15 in magnitude for both Passband and Stopband

### 3.2 Normalized Discrete Filter Specifications
- Passbands: \( 0 - \frac{\pi}{4} \) and \( \frac{11\pi}{30} - \pi \)
- Transition Bands: 0.016π on either side of passband
- Stopbands: \( \frac{4\pi}{15} \) to \( \frac{37\pi}{60} \)
- Tolerance: 0.15 in magnitude for both Passband and Stopband

### 3.3 Band-reject Filter using Kaiser Window
**Bandpass Characteristics**:

| Data  | Value   |
|-------|---------|
| ∆ω1   | 0.0523  |
| ∆ω2   | 0.0523  |
| N     | 41.0    |
| A     | 16.478  |
| α     | 0       |
| ωc1   | 0.811   |
| ωc2   | 1.96    |
| β     | 0.0     |

The ideal band-reject filter and consequent calculation are given by:

\[ h_{\text{ideal}} = \frac{\sin(\omega_{c2}k) - \sin(\omega_{c1}k)}{\pi k} \quad \text{for } k \in \{-N, -N + 1, \ldots, N - 1, N\} \]

\[ h_{\text{kaiser}} = w_K(2N + 1) \]

\[ h_{\text{bp}} = h_{\text{ideal}} \cdot h_{\text{kaiser}} \]

![Bandstop Filter](bandstop_filter.png)
*Figure 2: (a) Filter Coefficients (b) Frequency Response*

## 4. Cascade System
The frequency response of the cascaded filter can be obtained by multiplying the frequency response of the bandpass and the bandstop filter.

![Cascade Filter](cascade_filter.png)
*Figure 3: (a) Filter Coefficients (b) Frequency Response*
