# Speech Feature Extractions

- [Speech Feature Extractions](#speech-feature-extractions)
  - [Acoustic Features](#acoustic-features)
    - [Pause-based Features](#pause-based-features)
    - [Speaking Rate Features](#speaking-rate-features)
    - [Frequency Features](#frequency-features)
    - [Intensity Features](#intensity-features)
    - [ASR-based Features](#asr-based-features)
  - [Linguistic Features](#linguistic-features)
    - [Complexity Features](#complexity-features)
    - [Part-of-Speech (POS) based Features](#part-of-speech-pos-based-features)
    - [Perplexity Features](#perplexity-features)
  - [Conversation Features](#conversation-features)
    - [Hesitation and Puzzlement Features](#hesitation-and-puzzlement-features)
    - [Repetition Features](#repetition-features)
    - [Turn-related Features](#turn-related-features)

## Acoustic Features

### Pause-based Features

The pauses, including silent pauses, filled pauses (like um, hm, er, etc.), and non-verbal phenomena (like coughing, throat clearing, laughs, inspirations).
The related features include speech or pause duration, pause count, rate (such as words-per-minute (WPM)), speech period and the ratios between pauses and speeches.

The occurrence and duration of silence and speech segments can be captured by Voice Activity Detection (VAD) method in [Kaldi/ivector/voice-activity-detection](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/ivector/voice-activity-detection.cc), [Py-WebRTC-VAD](https://github.com/wiseman/py-webrtcvad), or [pyannote-audio](https://github.com/pyannote/pyannote-audio) for neural building blocks.

- [ ] Filled pauses detection

### Speaking Rate Features
****
### Frequency Features

### Intensity Features

### ASR-based Features

## Linguistic Features

### Complexity Features

### Part-of-Speech (POS) based Features

### Perplexity Features

## Conversation Features

### Hesitation and Puzzlement Features

### Repetition Features

### Turn-related Features
