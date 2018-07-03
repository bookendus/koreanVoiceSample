## koreanVoiceSample

This project is based on https://github.com/GSByeon/multi-speaker-tacotron-tensorflow  

To make Korean Voice Sample data like ljspeech (https://keithito.com/LJ-Speech-Dataset/) 

### Generate custom datasets

The `datasets` directory should look like:

    datasets
    ├── default
    │   ├── metadata.csv
    │   └── wavs
    │       ├── 1.wav
    │       ├── 2.wav
    │       ├── 3.wav
    │       └── ...


Metadata.csv contains:
   wav-filesname|text|text-normalization




## Install

python pip install -r requirements.txt 

python -c "import nltk; nltk.download('punkt')"

## if you use windows, ffmpeg is needed

http://adaptivesamples.com/how-to-install-ffmpeg-on-windows/

## if you have problem while install hangulize, check the link below

https://github.com/sublee/hangulize


## Usage

Each script execute below commands. (explain with son dataset)

1. To automate an alignment between sounds and texts, prepare GOOGLE_APPLICATION_CREDENTIALS to use Google Speech Recognition API. To get credentials, read this.

export GOOGLE_APPLICATION_CREDENTIALS="YOUR-GOOGLE.CREDENTIALS.json"


2. Download speech(or video) and text.

python -m dataproc.download


3. Segment all audios on silence.

python -m audio.silence --audio_pattern "./datasets/default/wavs/*.wav" --method=pydub


4. By using Google Speech Recognition API, we predict sentences for all segmented audios.

python -m recognition.google --audio_pattern "./datasets/default/wavs/*.*.wav"

5. Normailize korean text (ex, number )

python -m recognition.normalize --recognition_path "./datasets/default/recognition.json"

6. Finally, generated numpy files which will be used in training.

python3 -m datasets.generate_data ./datasets/default/metadata.csv





