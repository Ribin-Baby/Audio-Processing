 # Audio Processing Tutorial Book
---

## >> Tools used:
---

[![pyhton](https://www.python.org/static/community_logos/python-logo.png)](https://www.python.org/downloads/release/python-3715/)   [![librosa](https://librosa.org/images/librosa_logo_text.png)](https://librosa.org/)   [![pydub](https://images.g2crowd.com/uploads/product/image/large_detail/large_detail_86c4f17e5b0c4fc3d86420b9c7c5894c/pydub.png)](https://pydub.com/) 

[![numpy](https://ebssistemas.com/file/2021/05/NumPy-200x80.png)](https://numpy.org/)  [![matplotlib](https://matplotlib.org/2.0.2/plot_directive/mpl_examples/api/thumbnails/logo2.png)](https://matplotlib.org/stable/index.html)

## >> Installing tools:
---
1. <b>python</b>
 ```python
 Python 3.7.15
```
2.  <b>pydub</b>
```python
 pip install pydub==0.25.1 
```
3. <b> librosa </b> 
 ```python
 pip install librosa==0.8.1
```
4. <b>numpy</b>
 ```python
 pip install numpy==1.21.6
```
5. <b>matplotlib</b>
 ```python
 pip install matplotlib==3.2.2
```
<br>

1. ## >>> Reading Audio file
* We read audio files using `librosa` python package. Librosa is a tool used for music and audio analysis and processing.

* its a `4 second` audio with `sample rate : 22050 samples / second`.
*  sample plot of the audio signal is given below:
  
[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/1.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)

* the original audio is displayed below:

[audio sample](https://user-images.githubusercontent.com/115212881/197967862-03e34890-4536-455e-9aad-b1eba1094514.mov)



2. ## >>> Voice Activity Detection (VAT) and audio clipping.
* Voice activity detection (VAD) is **a technique in which the presence or absence of human speech is detected**.
* We begin by normalising the audio signal so that its amplitude falls between -1 and +1.  
* Next, we assign a threshold value above which when the signal goes, it will be a speech signal and all other below are noises and thus not considered.
* Through this process, we select our area of interest from the audio sample, and from that index range, we clip the audio and generate the desired output.
*   sample plot of the audio signal after VAD  and clipping is given below:
  
[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/2.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)

* the red graph is the VAD plot and the blue one is the audio signal.
* The area where the red pulse occured is our area of interest.
* after selecting the range we will clip the audio sample in that selected range, a cropped audio signal plot is given below:
[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/3.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)
* so after cropping the audio only contains speech / human voice the silent part gets removed and thus the duration also gets reduced.
*  the cropped audio / audio after clipping is displayed below:

[audio sample](https://user-images.githubusercontent.com/115212881/197990158-d0e9e4ae-dddc-44f0-9988-dbad54480c6b.mov)


3. ## >>> Pre-Emphasis
* The first step is to apply a pre-emphasis filter on the signal to amplify the high frequencies. A pre-emphasis filter is useful in several ways: (1) balance the frequency spectrum since high frequencies usually have smaller magnitudes compared to lower frequencies, (2) avoid numerical problems during the Fourier transform operation and (3) may also improve the Signal-to-Noise Ratio (SNR).

The pre-emphasis filter can be applied to a signal  `x`  using the first order filter in the following equation:

$y(t)=x(t)−αx(t−1)$

* where `α` is the filter coefficient we take its value as `0.97` in most of the cases.
*   sample plot of the audio signal after pre-emphasis is given below:
  
[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/4.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)

* pre-emphasised audio is displayed below:


[audio sample](https://user-images.githubusercontent.com/115212881/197996125-94f82bd4-176d-49c1-b9a7-53e48fe9fa2c.mov)

4. ## >>> sampling audio signal
* first of all we are splitting the audio signal or applying a sliding window to the audio signal so that we will get `n`- number of audio samples of equal time duration / intervals (we are taking `10ms` audio samples).

*   full audio signal as continuous plots of `10ms` samples is given below:
  
[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/frame.gif)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images/frame.gif)

* a single audio sample will looks like this:

[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/6.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)


5. ## >>> applying hann-window function to each audio samples
* We use the hann-window function to limit spectrum leakage, smooth the beginning and end of each audio sample we previously prepared, and challenge the FFT's assumption that the data is endless.
* The following equation generates the coefficients of a Hann window:

> $w(n)=0.5(1−cos(2πnN)),0≤n≤N$

> The window length  $L =  N  + 1$.

*   full audio signal as continuous plots of `10ms` samples  after applying hann-window function is given below:
  
![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/windows.gif)
* a single audio sample  after applying hann-window function will looks like this:

[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/7.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)


* audio signal after applying window function is dispalyed below:

[audio sample](https://user-images.githubusercontent.com/115212881/198013223-fdf9dc17-0994-4526-ba01-409dc48aa690.mov)

6. ## >>> time domain to frequency domain conversion of audio signal
* we use Fast Fourier Transform (FFT) to do this conversion task. 
* after this conversion a signal in time domain will be converted to frequency domain. 

*   audio signal in `time domain ( X-axis time )` is shown below:
  
![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/1.png)
* Audio signal after applying FFT , now in `frequency domain (X-axis frequency)` is shown below:

[![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/5.png)](https://github.com/Ribin-Baby/Audio-Processing/tree/main/images)

7. ## >>> `spectrogram` of the audio signal
* A spectrogram is a visual representation of the spectrum of frequencies of a signal as it varies with time. It’s a representation of frequencies changing with respect to time for given audio signals.
* In spectrogram we have time in `X-axis` and frequency in `Y-axis`.


*   audio signal `spectrogram` is shown below:
  
![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/9.png)
* The colour intensity shows the variation in power level of audio signal in `(dB)`, red colour indicates more power and blue indicates low power areas.

8. ## >>> `MFCC` ( Mel-frequency Cepstral Coefficients ) feature extraction
* mel-scale comes from the fact that human ear is highly sensitive to small changes made in the low frequency components. mel-scale is almost linear for frequency below 1000 Hz, and logarithmic for frequency above 1000 Hz, thus following the same pattern as that of the human ear.
* The [mel frequency cepstral coefficients](https://en.wikipedia.org/wiki/Mel-frequency_cepstrum) (MFCCs) of a signal are a small set of features (usually about 10-20) which concisely describe the overall shape of a spectral envelope.
* MFCC features are widely used in speech recognition problems. Speech is dictated by the way in which we use our oral anatomy to create each sound. Therefore, one way to uniquely identify a sound (independent of the speaker) is to create a mathematical representation that encodes the physical mechanics of spoken language. MFCC features are one approach to encoding this information.
* In MFCC plot we have time in `X-axis` and `n` number of MFCC features  in `Y-axis` in our case it is `12` only.


*   `MFCC` feature plot is shown below:
  
![orginal audio signal](https://raw.githubusercontent.com/Ribin-Baby/Audio-Processing/main/images/11.png)

9. ## >>> Reconstruction of audio from MFCC features
* We can rebuild our original signal from MFCCs up to a certain degree even if they are a very compressed version of our original audio signal; nonetheless, acceptable losses must be taken into account.
*  a reconstructed version of above audio signal is displayed below:

[audio sample](https://user-images.githubusercontent.com/115212881/198025434-f1d60eb5-5f70-449c-9f84-c630980dee05.mov)

### THE END
___







