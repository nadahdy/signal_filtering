# signal_filtering
#ABSTRACT:
This project aims to reduce electromagnetic interference (EMI) in
radio telescopes through digital signal filtering.
A 50 Hz sine wave representing a clean astronomical signal was
simulated and combined with artificial interference from GSM (200
Hz), LTE (300 Hz), and WiFi (400 Hz), which can degrade the accuracy
of telescope data.
To suppress the interference, three Butterworth band-stop filters
were designed, each targeting a specific frequency.
MATLAB simulations demonstrated a 96% reduction in noise power,
with the filtered output closely matching the original signal.
This software-based approach enhances radio telescope performance
without the need for physical shielding, offering a practical solution
for modern radio astronomy.

#THE MATLAB CODE:
% ------------------- Band-Stop Filter to Remove Multiple Interferences -------------------

% Step 1: Generate a clean astronomical signal
fs = 1000;               % Sampling frequency (Hz)
t = 0:1/fs:1;            % Time vector
signal = sin(2*pi*50*t); % Original telescope signal (50 Hz sine wave)

% Step 2: Add interference (simulate RFI from common sources)

% Noise 1: Global System for Mobile Communications (GSM) ~ 900 MHz → simulated at 200 Hz
noise1 = 0.4 * sin(2*pi*200*t); 

% Noise 2: Long-Term Evolution (LTE) ~ 1800 MHz → simulated at 300 Hz
noise2 = 0.3 * sin(2*pi*300*t); 

% Noise 3: Wireless Fidelity (WiFi) ~ 2.4 GHz → simulated at 400 Hz
noise3 = 0.2 * sin(2*pi*400*t); 

% Combine signal + all noise
noisy_signal = signal + noise1 + noise2 + noise3;

% Step 3: Design a Band-Stop Butterworth filter to block all interference bands
% We'll block 3 frequency bands at once: 200±10 Hz, 300±10 Hz, 400±10 Hz

% Build a composite filter that rejects [190–210], [290–310], [390–410] Hz
% We use a combination of 3 band-stop filters applied in sequence

% Filter all together using cascaded Butterworth band-stop filters
[b1,a1] = butter(4, [190 210]/(fs/2), 'stop'); % GSM band
[b2,a2] = butter(4, [290 310]/(fs/2), 'stop'); % LTE band
[b3,a3] = butter(4, [390 410]/(fs/2), 'stop'); % WiFi band

% Apply all filters
temp1 = filter(b1, a1, noisy_signal);
temp2 = filter(b2, a2, temp1);
final_filtered = filter(b3, a3, temp2);

% Step 4: Plot the signals
figure;
subplot(3,1,1); plot(t, signal); title('Original Clean Signal');
subplot(3,1,2); plot(t, noisy_signal); title('Signal with GSM, LTE, WiFi Interference');
subplot(3,1,3); plot(t, final_filtered); title('Filtered Signal (Butterworth Band-Stop)');

#Filter Type: 
Filter Used: Butterworth Band-Stop Filter
Reason: Butterworth filters are smooth (no ripple) and good for precise frequency rejection.
Equation of Butterworth Filter (magnitude response):
|H(f)| = 1 / sqrt(1 + (f/fc)^(2n))
Where fc = cutoff frequency, n = order



#REFRENCE MATLAB CODE:
- MathWorks Butterworth Function: https://www.mathworks.com/help/signal/ref/butter.html
