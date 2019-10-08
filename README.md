# Audio-Segmentation-by-Classification
 
Usually, to be classified, a sound is split into a sequence of very short overlapping frames from which we extract spectral and/or cepstral COEFFICIENTS (MFCC). 

When using a frame-level scheme, an aggregation strategy should be used. With GMM classifiers for instance, we would sum up the log likelihood of feature vectors the sound is made up of. The unknown sound is given the label of the GMM model that yields the highest sum of log likelihoods. Along with frame-level techniques, there are also segment-level techniques. SVM super vector-based approaches for instance transform a sequence of feature vectors into one huge vector (e.g. a super vector made up of stacked mean vectors of an adapted GMM Universal Background Model) that is classified by an SVM classifier.

auditok's core tokenization class, StreamTokenizer, takes a decision only based on the current frame. It calls the read() method of a DataSource object (the data of which are to be segmented/tokenized) to read a frame at once and asks its encapsulated validator if it is a valid frame or not. The log energy based validator that is part of the auditok package would simply compute the log energy of the given frame and return True if it is >= a user-defined threshold, False otherwise.

Clearly we don't want the GMM-based VALIDATOR to simply take a decision based on one single frame (though this would work for certain sound classes as we will see below). The solution to this problem is as follows: we implement a DataSource class that can not only return the current frame, but also the context of the frame with the desired scope. The context here stands for the k frames that are just before (i.e. history) and after (i.e. future) the current frame. Thus, each DataSource.read() can optionally (if scope > 0) return a sequence of vectors that the a GMM-based validator will score.

