# Audio Representations
## Pulse-Code Modulation (PCM)
A raw recording has several parameters:
- number of channels.
- bit depth.
- sampling rate.
## Mel Spectrogram
A Mel spectrogram shows how the energy of an audio spreads over frequency and time.
- if the audio is a single unchanging sound, we could run a single FFT to extract the sinusoidal waves that gave rise it.
- in practice the sound changes over time.
- a spectrogram runs many FFTs on overlapping windows.
- a mel spectrogram passes the frequencies through a frequency-to-mel map.

![](figures/mel-spectrogram.png)

# Whisper
Whisper is trained on multiple tasks:
- English transcription.
- Any-to-English speech translation.
- Non-English transcription.
- No speech.

![](figures/whisper.png)

# Gemini
Multimodal large language models (e.g. Gemini) are trained with many different modalities as input.

# AudioLM
AudioLM has 2 tokenizers:
- acoustic: SoundStream
- semantic: w2v-BERT

It generates audio tokens in 3 stages.

![](figures/audiolm.png)

# AudioLDM
AudioLDM uses a latent diffusion model to generate the Mel spectrogram.
![](figures/audioldm.png)

# Stable Audio
Stable Audio conditions on the start time and total time of the audio to enable variable length audio generation.

![](figures/stable-audio.png)

# Veo 3
Veo 3 is a video diffusion model that simultaneously diffuses audio.

![](figures/veo3.png)