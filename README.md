# Speech-to-Text-with-Watson-STT-and-Python

In this task I converted speech to voice using IBM Watson Speech to Text and Python, what is this service? IBM Watson Speech to Text (STT) is a service on the IBM Cloud that enables you to easily convert audio and voice into written text.

Steps:

1. Set up the IBM Watson Speech to Text service from https://cloud.ibm.com/catalog, and keep the key, link and region.

2. Open CMD or Visual Studio Code

3. Clone STT Code from https://github.com/IBM/watson-streaming-stt:
```
git clone  https://github.com/IBM/watson-streaming-stt
```

4. Add this code in transcribe.py page, under **def on_message(self, msg)**, to save the text to txt file:
```
        file = open('TranscribedText.txt', 'w')
        file.writelines(data['results'][0]['alternatives'][0]['transcript'])
```

5.  Install dependencies:
``` 
cd .\watson-streaming-stt
```
```
pip install -r requirements.txt
```

6. Install pipwin if errors on windows installing pyaudio: 
```
pip install pipwin
```
```
pipwin install pyaudio
```

7. update setup/config with APIKEY: go to file speech.cfg and paste your Apikey, and the used region, and make the file in .cfg extention only without .example extention.

8. run live transcription: 
```
python.transcribr.py -t 10
```
*10 means the time of the recording is 10 seconds


