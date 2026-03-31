# Communication System Components

## 1. Information Source

The origin of messages to be transmitted.

**Types:**

### (a) Discrete sequences
- **Example:** Telegraph/teletype
- Letters: "HELLO" → H-E-L-L-O

### (b) Single function of time
- **Example:** Radio/telephony
- Audio signal: f(t) = amplitude at time t
- Voice: continuous sound wave varying over time

### (c) Function of time + space (2D)
- **Example:** Black & white TV
- f(x, y, t) = brightness at position (x,y) at time t
- Each pixel's intensity changes over time

### (d) Multiple functions of time
- **Example:** Stereo audio (2 channels)
- Left: f(t), Right: g(t)
- Or multiplex: multiple independent channels

### (e) Multiple functions of multiple variables
- **Example:** Color TV
- Red: f(x, y, t)
- Green: g(x, y, t)
- Blue: h(x, y, t)
- Vector field in 3D space-time

### (f) Combinations
- **Example:** TV + audio
- Video: f(x, y, t) + Audio: g(t)

---

## 2. Transmitter

Converts message into transmittable signal.

**Examples:**
- **Telephony:** Sound pressure → electrical current
- **Telegraphy:** Letters → dots/dashes/spaces (encoding)
- **PCM multiplex:** Speech → sample → compress → quantize → encode → interleave
- **Vocoder:** Speech → parameters (pitch, formants, etc.)
- **FM radio:** Audio → frequency modulated carrier wave

---

## 3. Channel

The medium carrying the signal from transmitter to receiver.

**Examples:**
- Pair of wires
- Coaxial cable
- Radio frequency band
- Optical fiber (beam of light)
- Wireless spectrum

---

## 4. Receiver

Performs inverse operation of transmitter to reconstruct the message.

**Examples:**
- **Telephony:** Electrical current → sound pressure (speaker)
- **Telegraphy:** Dots/dashes → letters (decoding)
- **PCM:** Deinterleave → decode → expand → reconstruct speech
- **FM radio:** Demodulate carrier → audio signal

---

## 5. Destination

The intended recipient of the message.

**Examples:**
- Human listener (telephony, radio)
- Human viewer (television)
- Computer system (data transmission)
- Recording device
