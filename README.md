# Experimental verification of PSK and QPSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.
# Tools required
Google colab Python
# Theory
Phase Shift Keying (PSK) is a digital modulation technique in which the phase of a carrier signal changes according to binary data. In Binary PSK, two phases represent binary 0 and 1. Quadrature Phase Shift Keying (QPSK) uses four different phase shifts to transmit two bits per symbol, improving bandwidth efficiency. During demodulation, the original data is recovered using carrier synchronization. PSK and QPSK are widely used in modern digital communication systems for reliable data transmission.
# Program
# PSK

import numpy as np
import matplotlib.pyplot as plt
fs = 1000         
Tb = 1              
fc = 5              
data = [1,0,1,1,0,1]

t = np.arange(0, Tb, 1/fs)
message = np.repeat(data, len(t))
time = np.arange(len(message)) / fs
carrier = np.sin(2*np.pi*fc*time)
# 1 -> +1 , 0 -> -1
polar_data = 2*message - 1
psk = polar_data * carrier
demod = psk * carrier
reconstructed = (demod > 0).astype(int)
plt.figure(figsize=(12,8))

plt.subplot(4,1,1)
plt.plot(time, message)
plt.title("Message Signal")
plt.ylim(-0.5,1.5)
plt.grid()

plt.subplot(4,1,2)
plt.plot(time, carrier)
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(time, psk)
plt.title("PSK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(time, reconstructed)
plt.title("Demodulated Signal")
plt.ylim(-0.5,1.5)
plt.grid()

plt.tight_layout()
plt.show()



# QPSK

import numpy as np
import matplotlib.pyplot as plt

fs, Tb, fc = 1000, 1, 5
data = [1,0, 0,1, 1,1, 0,0]   # even bits

t = np.arange(0, Tb, 1/fs)
I = np.repeat(data[0::2], len(t))
Q = np.repeat(data[1::2], len(t))
time = np.arange(len(I))/fs
c1 = np.cos(2*np.pi*fc*time)
c2 = np.sin(2*np.pi*fc*time)
qpsk = (2*I-1)*c1 + (2*Q-1)*c2
I_rec = (qpsk*c1 > 0).astype(int)
Q_rec = (qpsk*c2 > 0).astype(int)

reconstructed = np.ravel(np.column_stack((I_rec, Q_rec)))

plt.figure(figsize=(12,8))

plt.subplot(4,1,1)
plt.plot(time, I)
plt.title("Message Signal")
plt.ylim(-0.5,1.5); plt.grid()

plt.subplot(4,1,2)
plt.plot(time, c1)
plt.title("Carrier Signal")
plt.grid()

plt.subplot(4,1,3)
plt.plot(time, qpsk)
plt.title("QPSK Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(time, reconstructed[:len(time)])
plt.title("Demodulated Signal")
plt.ylim(-0.5,1.5); plt.grid()

plt.tight_layout()
plt.show()

# Output Waveform
# PSK
<img width="1303" height="875" alt="Screenshot 2026-05-19 100903" src="https://github.com/user-attachments/assets/b8e91b54-3a09-4a82-badb-0a2f753fef62" />



# QPSK
<img width="1298" height="885" alt="Screenshot 2026-05-19 100952" src="https://github.com/user-attachments/assets/43ae0646-0c41-4918-a0eb-9adc80b751af" />



# Results
Thus the simple Python program for the modulation and demodulation of PSK and QPSK is done and verified.
