# Audio-Segmentation-by-Classification
Audio segmentation means at least two things:  Figure out, within an audio stream (audio file, network stream, audio device, etc.), regions that represent an audio activity (no matter what kind of activity) and those that represent a silence. This type of segmentation is rather referred to as Audio (or Acoustic) Activity Detection (AAD) and is a binary classification problem. Tell apart, within an audio stream, the nature of audio activities (e.g. speech, engine, bird, glass break, etc.). This is a multi-class classification problem. The former is a much simpler problem. In fact, if what we are looking for is to detect the presence of audio activities (of any kind), we can rely on simple parameters such as signal energy. auditok, a tool and API I published recently, can perfectly deal with this problem.  As for recognizing the nature of audio activities within an audio stream, this is a much more complex problem. Two kinds of schemes are used to deal with it: Segmentation then Classification or Segmentation by Classification.
