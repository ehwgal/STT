ASSIGNMENT 7
-----------
*by Ellemijn Galjaard*

This project is a fork of the [Coqui SST GitHub model](https://github.com/coqui-ai/STT), with an added notebook that fine-tunes this model.  
You can view the original README of the COQUI SST model under ``README.rst``.

About this Project
------------
- The notebook is located under the directory ``assignment7_ellemijn``. It runs a [COQUI STT model](https://github.com/coqui-ai/STT/blob/main/notebooks/train_personal_model_with_common_voice.ipynb) (which is a speech-to-text model trained on English audio data) and fine-tunes it on a self-recorded open-source [CommonVoice](https://commonvoice.mozilla.org/) dataset containing 230 .mp3 files. Each file contains a recording of one English sentence; all sentences were generated by CommonVoice. There is also a metadata file which links these .mp3 recordings to their transcriptions.

- **To run this project**, download or clone this github repository, and execute the notebook ``assignment7_ellemijn/fine-tune_model.ipynb``.  
This directory also contains two .txt files with results from an earlier run of the pre-trained model and fine-tuned model on the self-recorded CommonVoice test set.

- The files and metadata are downloaded via [gdown](https://pypi.org/project/gdown/) within the notebook itself. This was done so users are not required to mount their Drive to access this file when working in a Colab environment. This means that you only need to run the notebook (on Colab or locally) and have a working internet connection to run this project. A GPU is recommended.

- No ``requirements.txt`` file is provided, as the packages are installed within the notebook itself.

Results
------------

## Results of COQUI's pre-trained model on the self-recorded test set
The pre-trained model works surprisingly well on the self-recorded test set, as can be seen in ``assignment7_ellemijn/pre-trained_results.txt``. There is a Word Error Rate (WER) of around 15.8%, and the loss is only around 11.5%. The errors that were made by this model are also understandable. Take the following example:
- **original:** "shortly thereafter john's sister michelle darosa joined straylight run"
- **prediction:** "shortly thereafter joan sister michel de rosa joined stray light run"
This sentence has a WER of 66.7%, but virtually all of the mispredicted words are names.  
The same is true for this sentence:
- **original:** "miedema and evans then set each other up for the goals that followed"
- **prediction:** "my demand than stand sadeah other up for the girls that followed"
'Miedema' is not a particularly well-known name (especially in English), so it's no wonder that this word was mispredicted.  
There are other mistakes that do not include names (i.e. it identified "one stop shopping" as "once stopped chopping"), but in general the model performance is very good.

## Results of fine-tuned model on the self-recorded test set
As could be expected, the fine-tuned model performs better on the test set, as can be seen in ``assignment7_ellemijn/fine-tuned_results.txt``.
However, the improvement is only marginal: the WER is around 14.5% and the loss is around 10.7%.  
This is probably due to the fact that the model was fine-tuned with only 230 audio files, and might require more data to improve even further. 
As can be seen in the results, this model also appears to struggle the most with names, which is understandable:
- **original:** "as bill bryson says not all repetition is bad"
- **prediction:** "he still brissensis not all repetition is bad"

- **original:** "the film stars kapoor pran and padmini in lead roles"
- **prediction:** "the film stars caper pen and pudmini and lead rolls"

It also misidentified other words (i.e. "stores" as "sources"). One interesting misidentification is that it mispredicts "rival" as "rifle" -- this is a clear indication that it is not fine-tuned enough on my accent, as Dutch speakers (like myself) oftend tend to devoice 'v'. Presumably, it would correct this mistake had it been fine-tuned with more training data.

However, overall the results are very promising!