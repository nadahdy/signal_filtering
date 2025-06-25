# signal_filtering
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

REFRENCE MATLAB CODE:
- MathWorks Butterworth Function: https://www.mathworks.com/help/signal/ref/butter.html
