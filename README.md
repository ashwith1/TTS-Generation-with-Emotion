git clone https://github.com/ashwith1/TTS-Generation-with-Emotion.git

sudo apt-get install git-lfs
git lfs install

git clone https://huggingface.co/SWivid/E2-TTS
git clone https://huggingface.co/SWivid/F5-TTS

python3 -m venv venv
. venv/bin/activate
# Install pytorch with your CUDA version
pip install torch==2.4.1+cu124 torchaudio==2.4.1+cu124 --extra-index-url https://download.pytorch.org/whl/cu124
export LD_LIBRARY_PATH=/usr/local/lib/python3.11/dist-packages/nvidia/cudnn/lib:$LD_LIBRARY_PATH
sudo apt-get update && sudo apt-get install ffmpeg
sudo apt install libsndfile1
pip install tf-keras
pip install optimum

pip install -e .
> ```


## Inference

```bash
# Launch a Gradio app (web interface)
f5-tts_infer-gradio

# Specify the port/host
f5-tts_infer-gradio --port 7860 --host 0.0.0.0

# Launch a share link
f5-tts_infer-gradio --share
```



### 2. CLI Inference

```bash
# Run with flags
f5-tts_infer-cli --model F5TTS_v1_Base \
--ref_audio "provide_prompt_wav_path_here.wav" \
--ref_text "The content, subtitle or transcription of reference audio." \
--gen_text "Some text you want TTS model generate for you."

# Run with default setting. src/f5_tts/infer/examples/basic/basic.toml
f5-tts_infer-cli
# Or with your own .toml file
f5-tts_infer-cli -c custom.toml

# Multi voice. See src/f5_tts/infer/README.md
f5-tts_infer-cli -c src/f5_tts/infer/examples/multi/story.toml
```


### 2. With Gradio App

```bash
# Quick start with Gradio web interface
f5-tts_finetune-gradio
```

Read [training & finetuning guidance](src/f5_tts/train) for more instructions.



## Development

Use pre-commit to ensure code quality (will run linters and formatters automatically)

```bash
pip install pre-commit
pre-commit install
```

When making a pull request, before each commit, run: 

```bash
pre-commit run --all-files
```


## Citation
If our work and codebase is useful for you, please cite as:
```
@article{chen-etal-2024-f5tts,
      title={F5-TTS: A Fairytaler that Fakes Fluent and Faithful Speech with Flow Matching}, 
      author={Yushen Chen and Zhikang Niu and Ziyang Ma and Keqi Deng and Chunhui Wang and Jian Zhao and Kai Yu and Xie Chen},
      journal={arXiv preprint arXiv:2410.06885},
      year={2024},
}
```
## License

Our code is released under MIT License. The pre-trained models are licensed under the CC-BY-NC license due to the training data Emilia, which is an in-the-wild dataset. Sorry for any inconvenience this may cause.
