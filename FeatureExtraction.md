# Speech Feature Extractions

- [Speech Feature Extractions](#speech-feature-extractions)
  - [Acoustic Features](#acoustic-features)
    - [Pause-based Features](#pause-based-features)
    - [Frequency Features](#frequency-features)
    - [Intensity Features](#intensity-features)
    - [ASR-based Features](#asr-based-features)
  - [Linguistic Features](#linguistic-features)
    - [Tag-based Features](#tag-based-features)
    - [Complexity Features](#complexity-features)
    - [Perplexity Features](#perplexity-features)
  - [Conversation Features](#conversation-features)
    - [Hesitation and Puzzlement Features](#hesitation-and-puzzlement-features)
    - [Repetition Features](#repetition-features)
    - [Turn-related Features](#turn-related-features)
  - [ADReSS Challenge 2020](#adress-challenge-2020)

## Acoustic Features

### Pause-based Features

The pauses, including silent pauses, filled pauses (like um, hm, er, etc.), and non-verbal phenomena (like coughing, throat clearing, laughs, inspirations).
The related features include speech or pause duration, pause count, rate (such as words-per-minute (WPM)), speech period, silence-to-word ratio, and so on.

The occurrence and duration of silence and speech segments can be captured by Voice Activity Detection (VAD) method in [Kaldi](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/ivector/voice-activity-detection.cc), [Py-WebRTC-VAD](https://github.com/wiseman/py-webrtcvad), or [pyannote-audio](https://github.com/pyannote/pyannote-audio) for neural building blocks. The toolkits of word-based features, such as WPM, are listed in [Tags-based Features](#tags-based-features).

- [ ] Filled pauses detection

### Frequency Features

These features include the information of voice period (speech period), vocal stability (pitch, [jitter](https://www.cs.upc.edu/~nlp/papers/far_jit_07.pdf), spectral flatness), vocal organs (formants), and others (zero-crossing rate (ZCR), spectral centroid, etc.).

| Features             | Tools                          |
| -------------------- | ------------------------------ |
| pitch, jitter, harmonics | [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py#L129), [Perturbation_analysis](https://github.com/Mak-Sim/Troparion/tree/master/Perturbation_analysis), [FCN-F0](https://github.com/ardaillon/FCN-f0), |
| |[opensmile.pitchJitter](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/pitchJitter.cpp), [.pitchACF](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lldcore/pitchACF.cpp), [.harmonics](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/harmonics.cpp), [Praat](https://github.com/luffy-yu/pitch_jitter_shimmer)                         |
| spectral flatness    | [librosa.feature.spectral_flatness](https://librosa.org/librosa/generated/librosa.feature.spectral_flatness.html#librosa.feature.spectral_flatness)                      |
| ZCR   | [librosa.feature.zero_crossing_rate](https://librosa.org/librosa/generated/librosa.feature.zero_crossing_rate.html#librosa.feature.zero_crossing_rate), [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py)                           |
| spectral/tonal centroid   | [python_speech_features.ssc](https://python-speech-features.readthedocs.io/en/latest/index.html#python_speech_features.base.ssc), |
| |[librosa.feature.spectral_centroid](https://librosa.org/librosa/generated/librosa.feature.spectral_centroid.html#librosa.feature.spectral_centroid), [.tonnetz](https://librosa.org/librosa/generated/librosa.feature.tonnetz.html#librosa.feature.tonnetz) |

### Intensity Features

These features include the amplitude of speech or pauses, [shimmer](https://www.cs.upc.edu/~nlp/papers/far_jit_07.pdf), harmonics-to-noise ratio ([HNR](https://core.ac.uk/reader/82343096)), root-mean-square (RMS) energy, Mel-frequency cepstral coefficients (MFCCs), Filterbank energy, and so on.

| Features                | Tools                    |
| ----------------------- | ------------------------ |
| spectrogram, energy | [pyAudioAnalysis](https://github.com/tyiannak/pyAudioAnalysis/blob/0396495663de14b8a83fe666cefb9fbe098d1956/pyAudioAnalysis/ShortTermFeatures.py), [librosa.feature.rms](https://librosa.org/librosa/generated/librosa.feature.rms.html), [opensmile.lldcore](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lldcore)                      |
| shimmer, HNR            | [Perturbation_analysis](https://github.com/Mak-Sim/Troparion/tree/master/Perturbation_analysis), [opensmile.pitchJitter](https://github.com/naxingyu/opensmile/blob/bcaf89d048253e9519d758057f1e7a2176871a3d/src/lld/pitchJitter.cpp)                      |
| MFCC, Filterbank        | [librosa](https://librosa.org/librosa/generated/librosa.feature.mfcc.html), [python_speech_features](https://python-speech-features.readthedocs.io/en/latest/index.html#python_speech_features.base.fbank) |

### ASR-based Features

| Features | Tools |
| -------- | ----- |
| i-vector | [kaldi-ivector](https://github.com/idiap/kaldi-ivector), [voxceleb-ivector](https://github.com/swshon/voxceleb-ivector)   |
| d-vector | [Real-Time Voice Cloning](https://github.com/CorentinJ/Real-Time-Voice-Cloning), [deep-speaker](https://github.com/philipperemy/deep-speaker)   |
| x-vector | [x-vector-kaldi-tf](https://github.com/hsn-zeinali/x-vector-kaldi-tf)   |

## Linguistic Features

### Tag-based Features

The tags include part-of-speech (POS), named entity, and dependency tags.
A similar feature is Linguistic Inquiry and Word Count (LIWC), which uses a dictionary to assign categories to words.

An anthology of annotation-tools can be found in [awesome-NLP](https://github.com/keon/awesome-nlp#annotation-tools). Specificly, the tagger toolkits for English and Chinese are listed below.

| Features | Tools for English | Tools for Chinese |
| -------- | ----------------- | ----------------- |
| Tags     | [NLTK](https://www.nltk.org/api/nltk.tag.html), [Stanford-CoreNLP](https://github.com/Lynten/stanford-corenlp), [StAn](https://github.com/ChristophAlt/StAn), [TextBlob](https://github.com/sloria/TextBlob) | [NLTK](https://www.nltk.org/api/nltk.tag.html), [HanLP](https://github.com/hankcs/HanLP/tree/master), [jieba](https://github.com/fxsjy/jieba) |
| LIWC | [LIWC-text-analysis](https://pypi.org/project/liwc-text-analysis/) | [Chinese LIWC](https://github.com/thunlp/Auto_CLIWC) |

### Complexity Features

Complexity features measure the lexical richness of texts, i.e. the variety of words and word combinations. The features include Brunet’s W index (use sample size and vocabulary size), Honoré’s R Statistics (use part of the frequency spectrum), standardized word entropy suffix ratio, and so on.

| Features    | Tools |
| ----------- | ----- |
| complexity  | [cophi](https://pypi.org/project/cophi/), [Linguistic-and-Stylistic-Complexity](https://github.com/tsproisl/Linguistic_and_Stylistic_Complexity) |
| readability | [textstat](https://github.com/shivam5992/textstat) |

### Perplexity Features

Perplexity features measure how well the language model fits the text. These features can be calculated by [NLTK](https://www.nltk.org/api/nltk.lm.html?highlight=perplexity#nltk.lm.api.LanguageModel.perplexity) toolkit. And there are also some examples such as [LangModel](https://github.com/ollie283/language-models/blob/master/LangModel.py) and [ChineseBERT](https://github.com/DUTANGx/Chinese-BERT-as-language-model).

## Conversation Features

A detailed conversational analysis toolkit by CornellNLP is [ConvoKit](https://github.com/CornellNLP/Cornell-Conversational-Analysis-Toolkit), including Linguistic coordination, diversity and so on.

### Hesitation and Puzzlement Features

These features include pause ratio/count (same as [Pause-based Features](#pause-based-features) above), question ratio (question words), incomplete sentence ratio, unintelligible word ratio (readability toolkit [textstat](https://github.com/shivam5992/textstat)) and so on.

- [ ] question ratio, incomplete sentence ratio

### Repetition Features

These features measures the frequency of repetitions, such as type-token ratio (can be extracted by [cophi](https://pypi.org/project/cophi/) and [Linguistic-and-Stylistic-Complexity](https://github.com/tsproisl/Linguistic_and_Stylistic_Complexity)) and so on.

### Turn-related Features

These features include number of unique words (type-token ratio in [Repetition Features](#repetition-features)) and response time/length (VAD in [Pause-based Features](#pause-based-features)) in a turn, the number of turns, average length of turns, and so on.

## ADReSS Challenge 2020

The baseline features in [ADReSS Challenge 2020](https://arxiv.org/abs/2004.06833) are including ComParE (extracted by [openSMILE](https://www.audeering.com/opensmile/)) and linguistic (extracted by [CLAN](https://dali.talkbank.org/clan/)).
