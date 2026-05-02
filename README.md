# jetson_setup


sudo apt update
sudo apt install flatpak -y
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub org.chromium.Chromium


Installing jetpack 6.2.2
sudo gedit /etc/apt/sources.list.d/nvidia-l4t-apt-source.list    --> change all repo versions to r36.5 in this file

sudo apt update
sudo apt dist-upgrade
sudo apt install --fix-broken -o Dpkg::Options::="--force-overwrite"


Install llama server locally
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp
cmake -B build
cmake --build build -j --target llama-server llama-cli


# Start a local OpenAI-compatib	le server with a web UI
./build/bin/llama-server -hf unsloth/gemma-4-E4B-it-GGUF:Q4_K_M

# Run inference directly in the terminal:
./build/bin/llama-cli -hf unsloth/gemma-4-E4B-it-GGUF:Q4_K_M



sudo docker run -it --runtime=nvidia --network host -v $HOME/.cache/huggingface:/root/.cache/huggingface ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin llama-server -hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M -t 8 -c 9024 -n 5024 --keep 2056 -ngl 999 --chat-template-kwargs '{"enable_thinking":false}'



sudo docker run -it --runtime=nvidia --network host -v $HOME/.cache/huggingface:/root/.cache/huggingface ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin llama-server -hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M -t 8 -c 19024 -n 5024 --keep 2056 -ngl 999 --chat-template-kwargs '{"enable_thinking":true}'


sudo docker run -it --runtime=nvidia --network host -v $HOME/.cache/huggingface:/root/.cache/huggingface ghcr.io/nvidia-ai-iot/llama_cpp:latest-jetson-orin llama-server -hf unsloth/gemma-4-E2B-it-GGUF:Q3_K_M -t 6 -c 55024 -n 15024 --keep 2056 -ngl 70 --chat-template-kwargs '{"enable_thinking":false}' --host 0.0.0.0 --port 8080




Used  system Message from : https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/Anthropic/Sonnet%204.5%20Prompt.txt
