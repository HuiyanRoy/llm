# Running a Local Granite Code model with 128K context length on MacBook using Ollama

There are different ways to host a local LLM, such as using **ilab** or **Ollama**. If you want to benefit from a **larger context window (e.g., 128K)**, this guide shows how to do it using **Ollama**.

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
In a new console window, download and run **IBM Granite models**, such as **granite-code:3b** or **granite3.2:8b**, which support **128K context window**.
Granite-code models are designed for code related tasks. 
```sh
ollama run granite-code:3b
```

Use the following command to download and run the newest Granite 3.2 model of 8 billion parameters, which is designed for a broader range of tasks beyond coding.
```sh
ollama run granite3.2:8b
```
⚠️ **Note:** Attempt of deploying **granite-34b** models ran into Out of Memory (OOM) errors on a MacBook Pro M1 Max (10-core CPU, 24/32-core GPU, 32GB memory). 

## 4. Chat with the Model
Once the model is running, you can start chatting:
```sh
>>> could you please create C++ code implementing QuickSort algorithm
```
Example response:
```cpp
Sure! Here's an example C++ code that implements QuickSort:
...
```

## 5. Running Other Models

To pull and use different models, such as **Mistral**:
```sh
ollama pull mistral
```

Other available models:
- **Llama 2** (7B, 13B, 70B)
- **Gemma**
- **Mistral**

## 6. Listing downloaded models
```sh
ollama list
```
Output

```sh
NAME               ID              SIZE      MODIFIED       
granite3.2:8b      9bcb3335083f    4.9 GB    14 minutes ago    
mistral:latest     f974a74358d6    4.1 GB    8 days ago        
granite-code:3b    becc94fe1876    2.0 GB    8 days ago   
```

## 7. Check the metadata of the models that you just installed to verify the context length is larger than 128000

Check the metadata of granite-code:3b model:
```sh
ollama show granite-code:3b
```
Output
```sh
Model
    architecture        llama     
    parameters          3.5B      
    context length      128000    
    embedding length    2560      
    quantization        Q4_0      

  Parameters
    stop    "System:"      
    stop    "Question:"    
    stop    "Answer:"      

  License
    Apache License               
    Version 2.0, January 2004 
```

Check the metadata of the granite3.2:8b model:

```sh
ollama show granite3.2:8b  
```
Output 
```sh
  Model
    architecture        granite    
    parameters          8.2B       
    context length      131072     
    embedding length    4096       
    quantization        Q4_K_M     

  License
    Apache License               
    Version 2.0, January 2004    

```

## 8. Exit
To exit the chat session, type:
```sh
>>> /bye
```

## Benefits
✅ **Protects Private Information** – Ensures intellectual property remains secure by running everything locally.  
✅ **Larger Context Window** – Supports up to **128K tokens** for better conversation continuity.  
✅ **Flexible Model Options** – Test and compare different LLMs for performance and output quality.  

---

This guide helps developers and AI practitioners effectively run **LLMs locally on a MacBook** while leveraging **IBM Granite** and other open-source models. 🚀
