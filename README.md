Forced Alignment using Montreal Forced Aligner (MFA)

IIIT Hyderabad – Speech Processing Assignment  
Author: Sammi Kumar

--------------------------------------------------

About the Project

This project was done as part of the Speech Processing assignment. The main
objective is to perform forced alignment between speech audio files and their
corresponding transcripts using Montreal Forced Aligner (MFA).

Forced alignment helps in finding the exact time when each word and phoneme
is spoken in the audio signal.

--------------------------------------------------

Dataset Description

The dataset contains 6 audio files in WAV format and 6 transcript files in
TXT format. Each transcript corresponds to one audio file.

Folder structure:

data/
  wav/
  transcripts/

--------------------------------------------------

System Setup

All experiments were carried out in a Kaggle Notebook environment using Conda.

MFA was installed using the following commands:

pip install condacolab
condacolab.install()

conda install -c conda-forge montreal-forced-aligner -y

Installation was verified using:

mfa version

--------------------------------------------------

Data Preparation

Before running MFA, the dataset was prepared in the required format.

The following steps were performed:

- The dataset was copied to the working directory
- All file names were converted to lowercase
- Audio and transcript files were matched
- A speaker folder was created

Final format:

mfa_data/speaker1/
  file.wav
  file.txt

This ensured that MFA could correctly process the data.

--------------------------------------------------

Models and Dictionary

The pretrained english_us_arpa acoustic and dictionary models were used.

For handling out-of-vocabulary words, a G2P model was also used to generate
a custom pronunciation dictionary.

Models were downloaded using:

mfa model download acoustic english_us_arpa
mfa model download dictionary english_us_arpa
mfa model download g2p english_us_arpa

--------------------------------------------------

Initial Alignment (Before OOV Handling)

Initial forced alignment was performed using the pretrained dictionary:

mfa align mfa_data english_us_arpa english_us_arpa aligned_before --clean

This step generated TextGrid files containing word and phoneme boundaries.

--------------------------------------------------

OOV Handling

Some words in the transcripts were not present in the default dictionary.
To handle this problem, a G2P model was used to generate pronunciations.

The custom dictionary was created using:

mfa g2p mfa_data english_us_arpa custom_dict.txt

--------------------------------------------------

Re-alignment (After OOV Handling)

After generating the custom dictionary, alignment was performed again:

mfa align mfa_data custom_dict.txt english_us_arpa aligned_after --clean

This improved the overall alignment quality.

--------------------------------------------------

Output Analysis

The final outputs were generated in the form of Praat TextGrid files.

Each TextGrid file contains word and phoneme tiers with their start and end
timestamps.

The files were inspected using the MFA inspect tool and by manually viewing
the TextGrid files.

--------------------------------------------------

Observations

Some minor timing mismatches were observed, especially in fast speech
segments. Background noise also affected a few phoneme boundaries.

After OOV handling, skipped words were reduced and alignment improved.

--------------------------------------------------

Conclusion

The forced alignment pipeline was successfully implemented using Montreal
Forced Aligner. The use of G2P for OOV handling helped in improving the final
results.

This project provided practical understanding of speech-text alignment.

--------------------------------------------------

Author

Name: Sammi Kumar  
Course: Speech Processing Assignment  

Institute: CSVTU BHILAI

