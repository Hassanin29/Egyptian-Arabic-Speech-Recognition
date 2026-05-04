# Egyptian-Arabic-Speech-Recognition
# Arabic Speech Recognition - Egyptian Dialect (Casablanca Dataset)

[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)
[![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-yellow.svg)](https://huggingface.co/)

## 📌 Overview

This project implements an Automatic Speech Recognition (ASR) system for Egyptian Arabic dialect using the Casablanca dataset. The system is built on a fine-tuned Whisper Tiny model, trained specifically to transcribe Egyptian Arabic speech to text.

## 🎯 Key Features

- **Language Focus**: Egyptian Arabic dialect recognition
- **Model Architecture**: OpenAI's Whisper Tiny (37M parameters)
- **Training Approach**: Encoder frozen, decoder fine-tuned
- **Performance Metrics**: 
  - Final WER (Word Error Rate): 0.8198
  - Final CER (Character Error Rate): 0.4636

## 📊 Dataset

The project uses the **UBC-NLP/Casablanca** dataset with the following characteristics:

- **Total Samples**: 846 audio files
- **Speaker Distribution**: 
  - Male: 699 samples
  - Female: 129 samples
- **Data Split**: 90% training (761 samples), 10% testing (85 samples)
- **Audio Format**: 16kHz sampling rate

## 🏗️ Project Structure
├── data_preprocessing/ # Dataset loading and preparation
├── feature_extraction/ # Log-Mel spectrogram extraction
├── model_training/ # Whisper fine-tuning implementation
├── evaluation/ # WER/CER calculation and analysis
├── model_saving/ # Model checkpoint management
└── notebooks/ # Jupyter notebooks for experimentation
## 🔧 Technical Implementation

### Preprocessing
- Audio resampling to 16kHz
- Log-Mel spectrogram extraction (128 mel bands)
- Dynamic padding for variable-length audio inputs
- Tokenization using Whisper processor

### Model Architecture
- **Base Model**: `openai/whisper-tiny`
- **Trainable Parameters**: 29.5M (decoder only)
- **Frozen Components**: Transformer encoder
- **Input Features**: Log-Mel spectrograms (128 × variable frames)

### Training Configuration
- **Batch Size**: 4
- **Initial Epochs**: 7
- **Additional Fine-tuning Epochs**: 5
- **Learning Rate**: 1e-4 (initial), 5e-5 (fine-tuning)
- **Optimizer**: AdamW

## 📈 Results
Initial Training (7 epochs): Loss: 0.0363 → WER: 1.1290
Additional Training (5 epochs): Loss: 0.0052 → WER: 0.8198
### Performance Improvement
- **WER Reduction**: 27.4% relative improvement
- **Loss Reduction**: 0.0461 initial → 0.0052 final

### Sample Transcriptions
Reference: ايوا يا سعد بس.
Prediction: ايوا يا سعد بس.
WER: 0.0000 ✓

Reference: ده نصاب دولي و مطلوب القبض عليه ده سارق من البنوك مية مليون دولار.
Prediction: هو ماكلف الأبدا عليه ده سرق من البنوك مية مية مليل ي دور؟
WER: 0.7500
