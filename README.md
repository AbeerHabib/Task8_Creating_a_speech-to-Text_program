# Creating a speech-to-text program using IBM Watson STT and Python

In this task, I utilized IBM Watson Speech to Text and Python to convert speech into voice. IBM Watson Speech to Text (STT) is a service on the IBM Cloud that enables you to easily convert audio and voice into written text.

## **Steps:**

1. Set up the IBM Watson Speech to Text service from https://cloud.ibm.com/catalog, and keep the key, link and region.

2. Open CMD or the terminal in Visual Studio Code.

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
python transcribe.py -t 10
```
*10 means the time of the recording is 10 seconds


**Result:**

![result1](https://user-images.githubusercontent.com/85819577/125170189-69304280-e1b6-11eb-8f26-4afc6212287b.png)
![result2](https://user-images.githubusercontent.com/85819577/125170192-6b929c80-e1b6-11eb-9828-4850af0f3738.png)




________________________________________________________________________________________________________________




**saving the text as mp3 file**

I was trying a lot to convert the text to audio, but it didn't work with me, everything was going ok but the mp3 file looking empty.

First, I added this part of the code at the beginning:

```
from ibm_watson import TextToSpeechV1
from ibm_cloud_sdk_core.authenticators import IAMAuthenticator
```
```
apikey = 'LNUptqkjVdfA7-3fLeddN0yhKiZDXDdmoqksjGcjsCQL'
url = 'https://api.us-south.speech-to-text.watson.cloud.ibm.com/instances/9d44702e-5e18-463b-950e-dae8d3bff813'        
```
```
authenticator = IAMAuthenticator(apikey)
tts = TextToSpeechV1(authenticator=authenticator)
tts.set_service_url(url) 
```

Then I add this code, it works to open the previously written text:
```
with open('./TranscribedText.txt', 'r') as f:
        text = f.readlines()
        text = [line.replace('\n', '') for line in text]
        text = ''.join(str(line) for line in text)
```

Then I added this code, and it converts text to audio:
```
with open('./voice.mp3', 'wb') as audio_file:
        res = tts.synthesize(text, accept='audio/mp3', voice='en-US_AllisonV3Voice').get_result()
        audio_file.write(result.content)
```


**Result:**


![stt](https://user-images.githubusercontent.com/85819577/126882386-77e6222f-374c-44ee-a84e-0a66cecf851e.png)
![text](https://user-images.githubusercontent.com/85819577/126882392-1b16c19f-25d8-4946-9e03-bba946df5231.png)

