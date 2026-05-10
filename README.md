# Jetson / Llama.cpp Setup Guide

## Install Flatpak and Chromium

```bash
sudo apt update
sudo apt install flatpak -y

flatpak remote-add --if-not-exists flathub \
https://flathub.org/repo/flathub.flatpakrepo

flatpak install flathub org.chromium.Chromium
```

---

# Installing JetPack 6.2.2

Edit NVIDIA apt sources:

```bash
sudo gedit /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

Change all repository versions to:

```text
r36.5
```

Then run:

```bash
sudo apt update
sudo apt dist-upgrade
sudo apt install --fix-broken -o Dpkg::Options::="--force-overwrite"
```

---

# Install llama.cpp Locally

Clone and build:

```bash
git clone https://github.com/ggerganov/llama.cpp.git

cd llama.cpp

cmake -B build
cmake --build build -j --target llama-server llama-cli
```

---

# Run llama.cpp Locally

## Start OpenAI-Compatible Server with Web UI

```bash
./build/bin/llama-server \
-hf unsloth/gemma-4-E4B-it-GGUF:Q4_K_M
```

## Run Inference in Terminal

```bash
./build/bin/llama-cli \
-hf unsloth/gemma-4-E4B-it-GGUF:Q4_K_M
```

---

# Docker-Based llama-server Commands

## Gemma 4 E2B Q3_K_M (Thinking Disabled)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M \
-t 8 \
-c 9024 \
-n 5024 \
--keep 2056 \
-ngl 999 \
--chat-template-kwargs '{"enable_thinking":false}'
```

---

## Gemma 4 E2B Q3_K_M (Thinking Enabled)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M \
-t 8 \
-c 19024 \
-n 5024 \
--keep 2056 \
-ngl 999 \
--chat-template-kwargs '{"enable_thinking":true}'
```

---

## Gemma 4 E2B Q3_K_M (Port 8080)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 100 \
--chat-template-kwargs '{"enable_thinking":false}' \
--jinja \
--host 0.0.0.0 \
--port 8080
```

---

## Gemma 4 E2B Q4_K_M (Stable Config)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q4_K_M \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 70 \
--chat-template-kwargs '{"enable_thinking":false}' \
--host 0.0.0.0 \
--port 8080
```

---

# Including Tool Call (Working Setup)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q4_K_M \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 70 \
--chat-template-kwargs '{"enable_thinking":true}' \
--jinja \
-fa 'on' \
--host 0.0.0.0 \
--port 8080:8080
```

---

# Enable Network Access from Other Devices

Check firewall status:

```bash
sudo ufw status
```

Allow port:

```bash
sudo ufw allow 8080/tcp
```

Enable firewall:

```bash
sudo ufw enable
```

---

# Gemma 4 E2B Q8_0

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf unsloth/gemma-4-E2B-it-GGUF:Q8_0 \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 70 \
--chat-template-kwargs '{"enable_thinking":true}' \
--host 0.0.0.0 \
--port 8080
```

---

# Google Gemma 4 E4B Assistant

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf google/gemma-4-E4B-it-assistant \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 70 \
--chat-template-kwargs '{"enable_thinking":true}' \
--host 0.0.0.0 \
--port 8080
```

---

# Gemma 4 31B Assistant GGUF (F16)

```bash
sudo docker run -it \
--runtime=nvidia \
--network host \
-v $HOME/.cache/huggingface:/root/.cache/huggingface \
ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin \
llama-server \
-hf Radamanthys11/Gemma-4-31B-it-assistant-GGUF:F16 \
-t 6 \
-c 55024 \
-n 15024 \
--keep 2056 \
-ngl 70 \
--chat-template-kwargs '{"enable_thinking":true}' \
--host 0.0.0.0 \
--port 8080
```

---

# Qwen 3.6 35B A3B

```bash
llama-server \
-hf unsloth/Qwen3.6-35B-A3B-GGUF:UD-Q2_K_XL
```

---

# System Prompt Reference

Used system message from:

https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/Anthropic/Sonnet%204.5%20Prompt.txt
