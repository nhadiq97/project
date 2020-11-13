# AIROBOT
Humanoid Robotic interface/ System Development for simplified control and managment based on intel Architectures

<h2>Overview / Usage</h2>
The project when complete creates and an easily replicatable completely offline robot with extended capabilities of Processing the environment and interacting accordingly. It could easily be used as a receptionist or a welcoming assistant or a home robot or if developed further even a robot that can aid in Hazardous operations.

<h2>Methodology / Approach</h2>
Speech Recognition: Speech to Text conversion on the basis of Baidu Deep speech model using Intel optimized tensorflow and trained with Audiobooks of at least 5000 Books and its text files alongside available open datasets available for speech training including the tedlium, mozilla speech corpus.

Image recognition: Derivative of Imagenet trained with a dataset of 5Million plus images and added gesture recognition capabilities. Using Tensorflow, Open CV.

The project shall primarily Be run on Devcloud to train huge datasets and then the trained model shall be executed on the robot utilizing Intel Processor based boards and Movidius NCS. Thereby considerably reducing the compute requirements and device cost, Power Requirement for the AI element in the robot.

Response system: A Self-developed and trained model to initiate responses and actions from self-learned or Online Responses to Refined and understood Queries.

Sensory Modules: The system utilizes Gyromagnetic domains to Balance the robot and at the same time record the coordinates and movements alongside Recognition of obstacles and mapping the space around 3dimentionally.

Robot Movement: Each degree of freedom and its movements are coupled and synchronized to work using twin Arduino mega boards externally controlled by our compute server(Upsquared board with Movidius)

<h2>Technologies Used</h2>
IOT, Embedded Computing, Movidius Neural Compute Stick, Theano, Tensorflow, OpenCV, Devcloud, Linux, Kinect Sensor, Openvino, DeepSpeech, Linux

<h2>Required hardware</h2>
Movidius Neural Compute stick-4
Realsense camera(or any other webcam)-1
Upsquared Developer board-1(preferably quad core models with atleast 8gb ram and ssd of 128gb)
Microphone (Multimicrophone array recomended)
Speaker- any bluetooth speaker
wifi module.

PyTorch implementation of convolutional networks-based text-to-speech synthesis models:

1. [arXiv:1710.07654](https://arxiv.org/abs/1710.07654): Deep Voice 3: Scaling Text-to-Speech with Convolutional Sequence Learning.
2. [arXiv:1710.08969](https://arxiv.org/abs/1710.08969): Efficiently Trainable Text-to-Speech System Based on Deep Convolutional Networks with Guided Attention.

Audio samples are available at https://r9y9.github.io/deepvoice3_pytorch/.

## Online TTS demo

Notebooks supposed to be executed on https://colab.research.google.com are available:

- [DeepVoice3: Single-speaker text-to-speech demo](https://colab.research.google.com/drive/1Yea4GJIx59bXMukNcElqvrWf61LANNsU)

## Highlights

- Convolutional sequence-to-sequence model with attention for text-to-speech synthesis
- Multi-speaker and single speaker versions of DeepVoice3
- Audio samples and pre-trained models
- Preprocessor for [LJSpeech (en)](https://keithito.com/LJ-Speech-Dataset/), [JSUT (jp)](https://sites.google.com/site/shinnosuketakamichi/publication/jsut) and [VCTK](http://homepages.inf.ed.ac.uk/jyamagis/page3/page58/page58.html) datasets, as well as [carpedm20/multi-speaker-tacotron-tensorflow](https://github.com/carpedm20/multi-Speaker-tacotron-tensorflow) compatible custom dataset (in JSON format)
- Language-dependent frontend text processor for English 

### Samples

- [Ja Step000380000 Predicted](https://soundcloud.com/user-623907374/ja-step000380000-predicted)
- [Ja Step000370000 Predicted](https://soundcloud.com/user-623907374/ja-step000370000-predicted)
- [Ko_single Step000410000 Predicted](https://soundcloud.com/user-623907374/ko-step000410000-predicted)
- [Ko_single Step000400000 Predicted](https://soundcloud.com/user-623907374/ko-step000400000-predicted)
- [Ko_multi Step001680000 Predicted](https://soundcloud.com/user-623907374/step001680000-predicted)
- [Ko_multi Step001700000 Predicted](https://soundcloud.com/user-623907374/step001700000-predicted)

## Notes on hyper parameters

- Default hyper parameters, used during preprocessing/training/synthesis stages, are turned for English TTS using LJSpeech dataset. You will have to change some of parameters if you want to try other datasets. See `hparams.py` for details.
- `builder` specifies which model you want to use. `deepvoice3`, `deepvoice3_multispeaker` [1] and `nyanko` [2] are surpprted.
- Hyper parameters described in DeepVoice3 paper for single speaker didn't work for LJSpeech dataset, so I changed a few things. Add dilated convolution, more channels, more layers and add guided attention loss, etc. See code for details. The changes are also applied for multi-speaker model.
- Multiple attention layers are hard to learn. Empirically, one or two (first and last) attention layers seems enough.
- With guided attention (see https://arxiv.org/abs/1710.08969), alignments get monotonic more quickly and reliably if we use multiple attention layers. With guided attention, I can confirm five attention layers get monotonic, though I cannot get speech quality improvements.
- Binary divergence (described in https://arxiv.org/abs/1710.08969) seems stabilizes training particularly for deep (> 10 layers) networks.
- Adam with step lr decay works. However, for deeper networks, I find Adam + noam's lr scheduler is more stable.

## Requirements

- Python 3 (<= 3.6)
- CUDA >= 8.0
- PyTorch >= v0.4.0

## Installation

Please install packages listed above first, and then https://github.com/nhadiq97/AIROBOT && cd AIROBOT/TTS
pip install -e ".[bin]"

## Getting started

### Preset parameters

There are many hyper parameters to be turned depends on what model and data you are working on. For typical datasets and models, parameters that known to work good (**preset**) are provided in the repository. See `presets` directory for details. Notice that

1. `preprocess.py`
2. `train.py`
3. `synthesis.py`

accepts `--preset=<json>` optional parameter, which specifies where to load preset parameters. If you are going to use preset parameters, then you must use same `--preset=<json>` throughout preprocessing, training and evaluation. e.g.,

```
python preprocess.py --preset=presets/deepvoice3_ljspeech.json ljspeech ~/data/LJSpeech-1.0
python train.py --preset=presets/deepvoice3_ljspeech.json --data-root=./data/ljspeech
```

instead of

```
python preprocess.py ljspeech ~/data/LJSpeech-1.0
# warning! this may use different hyper parameters used at preprocessing stage
python train.py --preset=presets/deepvoice3_ljspeech.json --data-root=./data/ljspeech
```

### 0. Download dataset

- LJSpeech (en): https://keithito.com/LJ-Speech-Dataset/
- VCTK (en): http://homepages.inf.ed.ac.uk/jyamagis/page3/page58/page58.html
- JSUT (jp): https://sites.google.com/site/shinnosuketakamichi/publication/jsut
- NIKL (ko) (**Need korean cellphone number to access it**): http://www.korean.go.kr/front/board/boardStandardView.do?board_id=4&mn_id=17&b_seq=464

### 1. Preprocessing

Usage:

```
python preprocess.py ${dataset_name} ${dataset_path} ${out_dir} --preset=<json>
```

Supported `${dataset_name}`s are:

- `ljspeech` (en, single speaker)
- `vctk` (en, multi-speaker)
- `jsut` (jp, single speaker)
- `nikl_m` (ko, multi-speaker)
- `nikl_s` (ko, single speaker)

Assuming you use preset parameters known to work good for LJSpeech dataset / DeepVoice3 and have data in `~/data/LJSpeech-1.0`, then you can preprocess data by:

```
python preprocess.py --preset=presets/deepvoice3_ljspeech.json ljspeech ~/data/LJSpeech-1.0/ ./data/ljspeech
```

When this is done, you will see extracted features (mel-spectrograms and linear spectrograms) in `./data/ljspeech`.

#### 1-1. Building custom dataset. (using json_meta)
Building your own dataset, with metadata in JSON format (compatible with [carpedm20/multi-speaker-tacotron-tensorflow](https://github.com/carpedm20/multi-Speaker-tacotron-tensorflow)) is currently supported.
Usage:

```
python preprocess.py json_meta ${list-of-JSON-metadata-paths} ${out_dir} --preset=<json>
```
You may need to modify pre-existing preset JSON file, especially `n_speakers`. For english multispeaker, start with `presets/deepvoice3_vctk.json`.

Assuming you have dataset A (Speaker A) and dataset B (Speaker B), each described in the JSON metadata file `./datasets/datasetA/alignment.json` and `./datasets/datasetB/alignment.json`, then you can preprocess  data by:

```
python preprocess.py json_meta "./datasets/datasetA/alignment.json,./datasets/datasetB/alignment.json" "./datasets/processed_A+B" --preset=(path to preset json file)
```

#### 1-2. Preprocessing custom english datasets with long silence. (Based on [vctk_preprocess](vctk_preprocess/))

Some dataset, especially automatically generated dataset may include long silence and undesirable leading/trailing noises, undermining the char-level seq2seq model.
(e.g. VCTK, although this is covered in vctk_preprocess)

To deal with the problem, `gentle_web_align.py` will
- **Prepare phoneme alignments for all utterances**
- Cut silences during preprocessing

`gentle_web_align.py` uses [Gentle](https://github.com/lowerquality/gentle), a kaldi based speech-text alignment tool. This accesses web-served Gentle application, aligns given sound segments with transcripts and converts the result to HTK-style label files, to be processed in `preprocess.py`. Gentle can be run in Linux/Mac/Windows(via Docker).

Preliminary results show that while HTK/festival/merlin-based method in `vctk_preprocess/prepare_vctk_labels.py` works better on VCTK, Gentle is more stable with audio clips with ambient noise. (e.g. movie excerpts)

Usage:
(Assuming Gentle is running at `localhost:8567` (Default when not specified))
1. When sound file and transcript files are saved in separate folders. (e.g. sound files are at `datasetA/wavs` and transcripts are at `datasetA/txts`)
```
python gentle_web_align.py -w "datasetA/wavs/*.wav" -t "datasetA/txts/*.txt" --server_addr=localhost --port=8567
```

2. When sound file and transcript files are saved in nested structure. (e.g. `datasetB/speakerN/blahblah.wav` and `datasetB/speakerN/blahblah.txt`)
```
python gentle_web_align.py --nested-directories="datasetB" --server_addr=localhost --port=8567
```
**Once you have phoneme alignment for each utterance, you can extract features by running `preprocess.py`**

### 2. Training

Usage:

```
python train.py --data-root=${data-root} --preset=<json> --hparams="parameters you may want to override"
```

Suppose you build a DeepVoice3-style model using LJSpeech dataset, then you can train your model by:

```
python train.py --preset=presets/deepvoice3_ljspeech.json --data-root=./data/ljspeech/
```

Model checkpoints (.pth) and alignments (.png) are saved in `./checkpoints` directory per 10000 steps by default.

#### NIKL

Pleae check [this](https://github.com/homink/deepvoice3_pytorch/blob/master/nikl_preprocess/README.md) in advance and follow the commands below.

```
python preprocess.py nikl_s ${your_nikl_root_path} data/nikl_s --preset=presets/deepvoice3_nikls.json

python train.py --data-root=./data/nikl_s --checkpoint-dir checkpoint_nikl_s --preset=presets/deepvoice3_nikls.json
```

### 4. Monitor with Tensorboard

Logs are dumped in `./log` directory by default. You can monitor logs by tensorboard:

```
tensorboard --logdir=log
```

### 5. Synthesize from a checkpoint

Given a list of text, `synthesis.py` synthesize audio signals from trained model. Usage is:

```
python synthesis.py ${checkpoint_path} ${text_list.txt} ${output_dir} --preset=<json>
```

Example test_list.txt:

```
Generative adversarial network or variational auto-encoder.
Once upon a time there was a dear little girl who was loved by every one who looked at her, but most of all by her grandmother, and there was nothing that she would not have given to the child.
A text-to-speech synthesis system typically consists of multiple stages, such as a text analysis frontend, an acoustic model and an audio synthesis module.


