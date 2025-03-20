```markdown
# TTS-Generation-with-Emotion

This repository provides a TTS generation system with emotion handling, built on top of F5-TTS and E2-TTS. It includes both inference and finetuning capabilities via CLI and a Gradio web interface.

## Repository Setup

Clone this repository:

```bash
git clone https://github.com/ashwith1/TTS-Generation-with-Emotion.git
cd TTS-Generation-with-Emotion
```

Install Git LFS (Large File Storage) for handling large files:

```bash
sudo apt-get install git-lfs
git lfs install
```

Clone the required model repositories:

```bash
git clone https://huggingface.co/SWivid/E2-TTS
git clone https://huggingface.co/SWivid/F5-TTS
```

## Environment Setup

Create and activate a Python virtual environment:

```bash
python3 -m venv venv
. venv/bin/activate
```

Install PyTorch with the CUDA version matching your system:

```bash
pip install torch==2.4.1+cu124 torchaudio==2.4.1+cu124 --extra-index-url https://download.pytorch.org/whl/cu124
```

Set the required environment variable for CUDA libraries:

```bash
export LD_LIBRARY_PATH=/usr/local/lib/python3.11/dist-packages/nvidia/cudnn/lib:$LD_LIBRARY_PATH
```

Update your system and install additional dependencies:

```bash
sudo apt-get update && sudo apt-get install ffmpeg
sudo apt install libsndfile1
```

Install the remaining Python dependencies:

```bash
pip install tf-keras
pip install optimum
```

Finally, install the repository in editable mode:

```bash
pip install -e .
```

## Inference

### 1. Gradio App (Web Interface)

Launch the Gradio web interface with the following commands:

- **Default launch:**

  ```bash
  f5-tts_infer-gradio
  ```

- **Specify port/host:**

  ```bash
  f5-tts_infer-gradio --port 7860 --host 0.0.0.0
  ```

- **Launch with a share link:**

  ```bash
  f5-tts_infer-gradio --share
  ```

### 2. CLI Inference

Run inference using the command-line interface with flags:

```bash
f5-tts_infer-cli --model F5TTS_v1_Base \
--ref_audio "provide_prompt_wav_path_here.wav" \
--ref_text "The content, subtitle or transcription of reference audio." \
--gen_text "Some text you want TTS model generate for you."
```

Alternatively, run with default settings:

```bash
f5-tts_infer-cli
```

Or use a custom configuration file:

```bash
f5-tts_infer-cli -c custom.toml
```

For multi-voice generation, check the example configuration:

```bash
f5-tts_infer-cli -c src/f5_tts/infer/examples/multi/story.toml
```

### 3. Finetuning with Gradio App

Start the finetuning interface with:

```bash
f5-tts_finetune-gradio
```

For more details, refer to the [training & finetuning guidance](src/f5_tts/train).

## Development

To ensure code quality, install and configure pre-commit:

```bash
pip install pre-commit
pre-commit install
```

Before each commit, run the pre-commit checks:

```bash
pre-commit run --all-files
```
