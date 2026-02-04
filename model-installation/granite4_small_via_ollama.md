# Running a Local Granite 4 Small model on MacBook using Ollama

This guide helps developers and AI practitioners run **LLMs locally on a MacBook** while leveraging **IBM Granite** and other open-source models.
There are different ways to host a local LLM, such as using **ilab**, **Ollama** or **vLLM**. This guide shows how to use **Ollama** to serve a granite 4 model locally.

## 1. Install Ollama
In a virtual environment on your MacBook, run:
```sh
brew install ollama
```
If you don't have Homebrew, install it first:
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 2. Start Ollama Server
Now, you should be able to run:
```sh
ollama serve
```

## 3. Download and Deploy LLM Models
In a new console window, download and run **IBM Granite models**, such as **granite4:small-h**.

```sh
ollama run granite4:small-h
```
There are also other models at your choice, eg:
```sh
ollama run granite4:tiny-h
```
Or 
```sh
ollama run granite4:micro-h
```
- **Note 1:** The models that will be pulled by ollama are typically the 4 bit quantized versions. By default, Ollama uses 4-bit quantization Q4_K_M to reduce memory usage and improve performance on consumer hardware. 
- **Note 2:** Attempt of deploying **granite3 34b models** ran into Out of Memory (OOM) errors on a MacBook Pro M1 Max (10-core CPU, 24/32-core GPU, 32GB memory). 

In case you get errors in ollama serve window like:
```sh
llama_model_load: error loading model: error loading model architecture: unknown model architecture: 'granitehybrid'
llama_model_load_from_file_impl: failed to load model
```
this could indicate that your ollama version is too old. Refresh ollama via brew install
```sh
brew install ollama
```

## 4. Chat with the Model
Once the model is running, you can start chatting:
```sh
>>> tell me about who you are
```
Example response:
```sh
I am an artificial intelligence developed by IBM to assist businesses in deriving insights from their data, facilitating decision-making processes. My primary function is to ...
```

## 5. Listing downloaded models
```sh
ollama list
```
Output

```sh
NAME                                                   ID              SIZE      MODIFIED       
granite4:small-h                                       2f8a7367d441    19 GB     15 minutes ago    
gpt-oss:20b                                            f2b8351c629c    13 GB     6 months ago      
hf.co/mrutkows/granite-4.0-tiny-preview-GGUF:Q4_K_M    e319f351cc96    4.0 GB    6 months ago      
hf.co/mrutkows/granite-4.0-tiny-preview-GGUF:Q4_0      0ac31c7aafdb    3.8 GB    6 months ago      
granite-code:8b                                        36c3c3b9683b    4.6 GB    10 months ago     
granite3.2:8b                                          9bcb3335083f    4.9 GB    10 months ago     
mistral:latest                                         f974a74358d6    4.1 GB    11 months ago     
granite-code:3b                                        becc94fe1876    2.0 GB    11 months ago   
```

## 6. Check the metadata of the models that you just installed to check the context length, number of parameters, etc.

Check the metadata of granite4:small-h model:
```sh
ollama show granite4:small-h
```
Grante4:small-h model supports 1 MiB context length
```sh
  Model
    architecture        granitehybrid    
    parameters          32.2B            
    context length      1048576          
    embedding length    4096             
    quantization        Q4_K_M           

  Capabilities
    completion    
    tools         

  License
    Apache License               
    Version 2.0, January 2004    
    ...   
```
## 7. Inference via python
To inference the model via your python code, run direct REST calls to Ollama’s local HTTP server (/api/chat, /api/generate, …). Example:
```bash
import requests

BASE = "http://localhost:11434"
MODEL = "granite4"  # replace with your exact model name from `ollama list`

payload = {
    "model": MODEL,
    "prompt": "Hello Granite 4",
    "stream": False
}

r = requests.post(f"{BASE}/api/generate", json=payload, timeout=120)
r.raise_for_status()
data = r.json()

print(data["response"])
```



## 8. Exit
To exit the chat session, type:
```sh
>>> /bye
```
