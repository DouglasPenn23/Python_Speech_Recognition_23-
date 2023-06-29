# Python_Speech_Recognition_23-
Repository for educating myself on using speech recognition with Python. 


$ pip install SpeechRecognition

Once installed, you should verify the installation by opening an interpreter session and typing:

>>> import speech_recognition as sr
>>> sr.__version__
'3.8.1'

____________________________________

All of the magic in SpeechRecognition happens with the Recognizer class.

The primary purpose of a Recognizer instance is, of course, to recognize speech. Each instance comes with a variety of settings and functionality for recognizing speech from an audio source.

Creating a Recognizer instance is easy. In your current interpreter session, just type:

>>> r = sr.Recognizer()

____________________________________
Type the following into your interpreter session to process the contents of the “harvard.wav” file:

harvard = sr.AudioFile('harvard.wav')
>>> with harvard as source:
...    audio = r.record(source)
...

>>> type(audio)
<class 'speech_recognition.AudioData'>

____________________________________

>>> with harvard as source:
...     audio = r.record(source, duration=4)
...
>>> r.recognize_google(audio)
'the stale smell of old beer lingers'

____________________________________

>>> with harvard as source:
...     audio1 = r.record(source, duration=4)
...     audio2 = r.record(source, duration=4)
...
>>> r.recognize_google(audio1)
'the stale smell of old beer lingers'
>>> r.recognize_google(audio2)
'it takes heat to bring out the odor a cold dip'



>>> with harvard as source:
...     audio = r.record(source, offset=4, duration=3)
...
>>> r.recognize_google(audio)
'it takes heat to bring out the odor'



>>> with harvard as source:
...     audio = r.record(source, offset=4.7, duration=2.8)
...
>>> r.recognize_google(audio)
'Mesquite to bring out the odor Aiko'


___________________________________________

Effect of noise on Speech Recognition 


>>> jackhammer = sr.AudioFile('jackhammer.wav')
>>> with jackhammer as source:
...     audio = r.record(source)
...
>>> r.recognize_google(audio)
'the snail smell of old gear vendors'


* Use adjust for ambient Noise Class

>>> with jackhammer as source:
...     r.adjust_for_ambient_noise(source)
...     audio = r.record(source)
...
>>> r.recognize_google(audio)
'still smell of old beer vendors'