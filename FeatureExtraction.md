# Speech Feature Extractions

- [Speech Feature Extractions](#speech-feature-extractions)
  - [Acoustic Features](#acoustic-features)
    - [Pause-based Features](#pause-based-features)
    - [Frequency Features](#frequency-features)
    - [Intensity Features](#intensity-features)
    - [ASR-based Features](#asr-based-features)
  - [Linguistic Features](#linguistic-features)
    - [Tags-based Features](#tags-based-features)
    - [Complexity Features](#complexity-features)
    - [Perplexity Features](#perplexity-features)
  - [Conversation Features](#conversation-features)
    - [Hesitation and Puzzlement Features](#hesitation-and-puzzlement-features)
    - [Repetition Features](#repetition-features)
    - [Turn-related Features](#turn-related-features)

## Acoustic Features

### Pause-based Features

The pauses, including silent pauses, filled pauses (like um, hm, er, etc.), and non-verbal phenomena (like coughing, throat clearing, laughs, inspirations).
The related features include speech or pause duration, pause count, rate (such as words-per-minute (WPM)), speech period, silence-to-word ratio, and so on.

The occurrence and duration of silence and speech segments can be captured by Voice Activity Detection (VAD) method in [Kaldi](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/ivector/voice-activity-detection.cc), [Py-WebRTC-VAD](https://github.com/wiseman/py-webrtcvad), or [pyannote-audio](https://github.com/pyannote/pyannote-audio) for neural building blocks.

- [ ] Filled pauses detection
- [ ] word count

### Frequency Features

These features include the information of voice period (speech period), vocal stability (pitch, [jitter](https://www.cs.upc.edu/~nlp/papers/far_jit_07.pdf), spectral flatness), vocal organs (formants), and others (zero-crossing rate (ZCR), spectral centroid, etc.).

| Features             | Tools                          |
| -------------------- | ------------------------------ |
| pitch, jitter | [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py#L129), [Perturbation_analysis](https://github.com/Mak-Sim/Troparion/tree/master/Perturbation_analysis), [FCN-F0](https://github.com/ardaillon/FCN-f0), [opensmile.pitchJitter](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/pitchJitter.cpp), [opensmile.pitchACF](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lldcore/pitchACF.cpp), [opensmile.harmonics](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/harmonics.cpp), [Praat](https://github.com/luffy-yu/pitch_jitter_shimmer)                         |
| spectral flatness    | [librosa.feature.spectral_flatness](https://librosa.org/librosa/generated/librosa.feature.spectral_flatness.html#librosa.feature.spectral_flatness)                      |
| zero-crossing rate   | [librosa.feature.zero_crossing_rate](https://librosa.org/librosa/generated/librosa.feature.zero_crossing_rate.html#librosa.feature.zero_crossing_rate), [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py)                           |
| spectral centroid, tonal centroid    | [python_speech_features.ssc](https://python-speech-features.readthedocs.io/en/latest/index.html#python_speech_features.base.ssc), [librosa.feature.spectral_centroid](https://librosa.org/librosa/generated/librosa.feature.spectral_centroid.html#librosa.feature.spectral_centroid), [librosa.feature.tonnetz](https://librosa.org/librosa/generated/librosa.feature.tonnetz.html#librosa.feature.tonnetz) |

### Intensity Features

These features include the amplitude of speech or pauses, [shimmer](https://www.cs.upc.edu/~nlp/papers/far_jit_07.pdf), harmonics-to-noise ratio ([HNR](https://core.ac.uk/reader/82343096)), root-mean-square (RMS) energy, Mel-frequency cepstral coefficients (MFCCs), Filterbank energy, and so on.

| Features                | Tools                    |
| ----------------------- | ------------------------ |
| spectrogram, chromagram, energy_entropy, RMS energy | [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py), [librosa.feature.rms](https://librosa.org/librosa/generated/librosa.feature.rms.html), [opensmile.lldcore](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lldcore)                      |
| shimmer, HNR            | [Perturbation_analysis](https://github.com/Mak-Sim/Troparion/tree/master/Perturbation_analysis), [opensmile.pitchJitter](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/pitchJitter.cpp)                      |
| MFCC, Filterbank        | [librosa](https://librosa.org/librosa/generated/librosa.feature.mfcc.html), [python_speech_features](https://python-speech-features.readthedocs.io/en/latest/index.html#python_speech_features.base.fbank) |

### ASR-based Features

| Features | Tools |
| -------- | ----- |
| i-vector | [kaldi-ivector](https://github.com/idiap/kaldi-ivector), [voxceleb-ivector](https://github.com/swshon/voxceleb-ivector)   |
| d-vector | [Real-Time Voice Cloning](https://github.com/CorentinJ/Real-Time-Voice-Cloning), [deep-speaker](https://github.com/philipperemy/deep-speaker)   |
| x-vector | [x-vector-kaldi-tf](https://github.com/hsn-zeinali/x-vector-kaldi-tf)   |

## Linguistic Features

### Tags-based Features

The tags include part-of-speech (POS), named entity, and dependency tags.
A similar feature is Linguistic Inquiry and Word Count (LIWC), which uses a dictionary to assign categories to words.

An anthology of annotation-tools can be found in [awesome-NLP](https://github.com/keon/awesome-nlp#annotation-tools). Specificly, the tagger toolkits include English version, such as [NLTK](https://www.nltk.org/api/nltk.tag.html), [Stanford-CoreNLP](https://github.com/Lynten/stanford-corenlp), [StAn](https://github.com/ChristophAlt/StAn), [TextBlob](https://github.com/sloria/TextBlob), and Chinese version, such as [HanLP](https://github.com/hankcs/HanLP/tree/master), [jieba](https://github.com/fxsjy/jieba), etc. For the LIWC text analysis, there are toolkits like [LIWC-text-analysis](https://pypi.org/project/liwc-text-analysis/) and [Chinese LIWC](https://github.com/thunlp/Auto_CLIWC).

### Complexity Features

Complexity features measure the variety of words and word combinations. The features include Brunet’s W index and Honoré’s R Statistics, standardized word entropy suffix ratio, and so on.

### Perplexity Features

Perplexity measures how well the language model fits the text.

## Conversation Features

### Hesitation and Puzzlement Features

These features include pause ratio/count (same as [Pause-based Features](#pause-based-features) above), question ratio (question words), incomplete sentence ratio, unintelligible word ratio and so on.

### Repetition Features

These features measures the frequency of repetitions, such as type-token ratio (the ratio of the number of unique words to the total number of words) and so on.

### Turn-related Features

These features include the number of turns, average length of turns, number of unique words and response time/length in a turn, and so on.
