# Bringing Open-sourced LLMs into SAP AI Core with Ollama and LocalAI
The open-source community surrounding Large Language Models (LLMs) is evolving rapidly, with new models, backends, libraries, and toolings constantly emerging. These developments enable the running of LLMs locally or on self-hosted environments. This repository serves as a guide on how to bring popular open-source Large Language Models (such as Llama 2, Mistral, Mixtral, Gemma, LlaVA, etc.) into SAP AI Core using widely adopted open-source LLM tools or backends.
- [Ollama](https://ollama.com/)
- [LocalAI](https://localai.io/)
- [llama.cpp](https://github.com/ggerganov/llama.cpp/tree/master/examples/server)
- [vLLM](https://docs.vllm.ai)

## Why running open-sourced LLMs with SAP AI Core?
+ Data Protection & Privacy
+ Security
+ Cost-effectiveness
+ Flexibility of choices for LLMs and LLM backends etc.
+ Making open-sourced LLMs enterprise ready

## Why leverage Ollama, LocalAI, llama.cpp and vLLM in SAP AI Core?
Ollama, LocalAI, llama.cpp and vLLM offer a comprehensive solution for running Large Language Models (LLMs) locally or in self-hosted environments. Their full stack capabilities include:
- Model Management: Dynamically pull or download LLMs from model repository through API during run-time (exclusive to Ollama and LocalAI. vLLM provides seamless integration with Hugging Face models)
- Running LLM efficiently with GPU Acceleration in SAP AI Core using open-source backends such as llama.cpp, vllm, transformer, exllama etc.
- Serving with OpenAI-compatible chat completions and embedding APIs. 
- Easy deployment and setup without the need of without the need for custom code deployment in SAP AI Core.
- Commercially viability: They are all under MIT licenses or Apache 2.0 License.
<br/>

<style>
table {
    width: 100%;
}

td:nth-child(1) {
    width: 20%;
}

td:nth-child(2),
td:nth-child(3) {
    width: 40%;
}
</style>
### Ollama vs LocalAI in context of SAP AI Core
|                                     | <a href="https://ollama.com"><img src="https://ollama.com/public/ollama.png" alt="Ollama" height="100"/><br/>Ollama</a>  | <a href="https://localai.io/"><img src="https://github.com/go-skynet/LocalAI/assets/2420543/0966aa2a-166e-4f99-a3e5-6c915fc997dd" alt="LocalAI" height="100"/><br/>LocalAI</a> |
|-------------------------------------|--------------------------------------------|-------------------------------------|
| Description                         |     "Ollama: Get up and running with Llama 2, Mistral, Gemma, and other large language models."                                                                   | "LocalAI is the free, Open Source OpenAI alternative. LocalAI act as a drop-in replacement REST API that’s compatible with OpenAI API specifications for local inferencing..." |
| AI Capabilities                     |     -Text generation<br/> -Vision<br/> -Text Embedding   | -Text generation<br/> -Vision<br/>  -Text Embedding<br/> -Speech to Text<br/> -Text to Speech<br/> -Image Generation |
| Installation & Setup                |    Easy installation and setup   | Assure to use the corresponding docker image or build with the right variables for GPU acceleration. |
| GPU Acceleration                    |    Automatically detect and apply GPU   | Supported. Require configuration on model |
| Model Management                    |    Easy built-in model management through CLI command or APIs   | [Experimental model gallery](https://localai.io/models/)<br/> May require additional configuration for GPU acceleration per model |
| Supported Backends                  |    llama.cpp   | multi-backend support and backend agnostic. Default backend as llama.cpp, also support extra backends such as vLLM, rwkv, huggingface transformer, bert, whisper.cpp etc. Please check its [model compatibility table](https://localai.io/model-compatibility/) for details  |
| Supported Models                    |     [Built-in Model Library](https://ollama.com/library)   | [Experimental Model Gallery](https://localai.io/models/) |
| Model Switching                     |    Seamless model switching with automatic memory management   | Supported |
| APIs                                |    -Model Management API</br>-OpenAI-compatible chat/complemtions API<br/>-Embedding API    | -Model Management API<br/>-Text Generation API</br>-OpenAI-compatible chat/complemtions API<br/>-Embedding API |
| Model Customization                 |    supported   |  supported  |
| License                              |    MIT   |     MIT |
<br/>

### llama.cpp vs vLLM in context of SAP AI Core
|                                     | <a href="https://github.com/ggerganov/llama.cpp"><img src="https://user-images.githubusercontent.com/1991296/230134379-7181e485-c521-4d23-a0d6-f7b3b61ba524.png" alt="llama.cpp" height="100"/><br/>llama.cpp</a>  | <a href="https://docs.vllm.ai/"><img src="https://raw.githubusercontent.com/vllm-project/vllm/main/docs/source/assets/logos/vllm-logo-text-light.png" alt="vLLM" height="100"/><br/>vLLM</a> |
|-------------------------------------|--------------------------------------------|-------------------------------------|
| Description                         | "The main goal of llama.cpp is to enable LLM inference with minimal setup and state-of-the-art performance on a wide variety of hardware - locally and in the cloud." | "A high-throughput and memory-efficient inference and serving engine for LLMs" |
| AI Capabilities                     |     -Text generation<br/> -Vision<br/> -Text Embedding   | -Text generation<br/> -Vision<br/>  -Text Embedding<br/> |
| Deployment & Setup                  |    Easy deployment via docker. Many [arguments](https://github.com/ggerganov/llama.cpp/tree/master/examples/server) to explore on starting llama.cpp server  | Easy deployment via docker. Many [engine arguments](https://docs.vllm.ai/en/latest/models/engine_args.html) on starting vllm.entrypoints.openai.api_server  |
| GPU Acceleration                    |    Supported   |  Supported  |
| Model Management                    |    Not supported. Need external tool(wget etc) to download models from Hugging Face  | Seamless integration with popular HuggingFace models |
| Supported Quantization                  |    1.5-bit, 2-bit, 3-bit, 4-bit, 5-bit, 6-bit, and 8-bit integer quantization   | GPTQ, AWQ, SqueezeLLM, FP8 KV Cache  |
| Supported Models                    |     https://github.com/ggerganov/llama.cpp > Supported models   | [Supported Model](https://docs.vllm.ai/en/latest/models/supported_models.html) |
| Model Switching                     |    Not supported. One deployment for one model.   | Not supported. One deployment for one model.  |
| APIs                                |    -OpenAI-compatible chat/complemtions API<br/>-Embedding API    | -OpenAI-compatible chat/complemtions API<br/>-Embedding API<br/> |
| License                   |    MIT  | Apache-2.0 license |

## How to bring open-sourced LLMs into SAP AI Core
In the following section, we see how to bring open-sourced LLMs into SAP AI Core with Ollama, LocalAI, llama.cpp and vLLM.

### Prerequistive
The following softwares are required to serve an AI model in SAP AI Core. Please follow [this tutorial](https://developers.sap.com/group.ai-core-get-started-basics.html) to provision and set up your own SAP AI Core if it is new to you, which will cover the list below.
#### 1. [Use Boosters for Free Tier Use of SAP AI Core and SAP AI Launchpad](https://developers.sap.com/group.ai-core-get-started-basics.html)

#### 2. [Set Up Tools to Connect With and Operate SAP AI Core](https://developers.sap.com/tutorials/ai-core-setup.html)

#### 3. [Generate a GitHub personal access token](https://developers.sap.com/tutorials/ai-core-helloworld.html) and [Onboard Github to SAP AI Core](https://developers.sap.com/tutorials/ai-core-helloworld.html)
Only take the steps about Generate a GitHub personal access token and Onboard Github to SAP AI Core. We'll fork this GitHub repository instead of creating a new one.

#### 4. Install Docker Desktop and create a personal Docker Registry
Instructions can be found [here](https://docs.docker.com/docker-hub/quickstart/), Step 1 to 4.
We recommend you to create an access token to be used in place of your password. Instructions on how to generate a token can be found [here](https://docs.docker.com/docker-hub/access-tokens/#create-an-access-token).

#### 5. Install Git and Visual Studio Code(Optional)
* **Install Git** by following the instructions [here](https://github.com/git-guides/install-git).
* Download and Install Visual Studio Code by following instructions [here](https://code.visualstudio.com/)

#### 6.Fork [the GitHub repository of btp-generative-ai-hub-use-cases](https://github.com/SAP-samples/btp-generative-ai-hub-use-cases)
Fork with [this url](https://github.com/SAP-samples/btp-generative-ai-hub-use-cases/fork) into your own github account. Set your forked repository to **private**, for it holds the credentials to your SAP AI Core instance, GitHub, Docker registry etc in run-time, which should not be publicly accessible.  

#### 7.Clone your forked repository
```sh
git clone <YOUR_FORKED_REPOSITORY_URL> 
```

#### 8.Setup a local Python3 environment
* **Download and Install Python3(>=3.7)** in your local environment from [here](https://www.python.org/downloads/) or other approachs.
* Create a virtual environment and install the dependencies
```sh
# Create a virtual env and install the dependencies 
cd btp-generative-ai-hub-use-cases/10-byom-oss-llm-ai-core
python3 -m venv oss-llm-env
source oss-llm-env/bin/activate
pip3 install -r byom-oss-llm-code/requirements.txt
```

### Perform the initial configurations for byom-oss-llm-ai-core application in SAP AI Core
Please follow and run the jupyter notebook [00-init-config.ipynb](byom-oss-llm-code/00-init-config.ipynb) to perform the initial configurations for byom-oss-llm-ai-core application in SAP AI Core. To run the run the jupyter notebook, you can use either [JupyterLab](https://jupyterlab.readthedocs.io/en/latest/getting_started/starting.html) or [Visual Studio Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)
```sh
# Start the JupyterLab
jupyter lab
```
- copy [byom-oss-llm-code/config.template.json](byom-oss-llm-code/config.template.json) and rename the copy as config.json under folder byom-oss-llm-code
- Review and update configurations in config.json
- Onboarding the github repository
- Create the application and sync
- Create the configurations for scenarios

### Option 1: (Recommended) Bring open-sourced LLMs into SAP AI Core with Ollama
Please follow the jupyter notebooks below to deploy and test **Ollama** in SAP AI Core.
- [01-deployment.ipynb](byom-oss-llm-code/ollama/01-deployment.ipynb)
- [02-ollama.ipynb](byom-oss-llm-code/ollama/02-ollama.ipynb)

### Option 2: Bring open-sourced LLMs into SAP AI Core with LocalAI
Please follow the jupyter notebooks below to deploy and test **LocalAI** in SAP AI Core.
- [01-deployment.ipynb](byom-oss-llm-code/ollama/01-deployment.ipynb)
- [02-ollama.ipynb](byom-oss-llm-code/ollama/02-ollama.ipynb)

### Option 3: Bring open-sourced LLMs into SAP AI Core with llama.cpp
Please follow the jupyter notebooks below to deploy and test **llama.cpp** in SAP AI Core.
- [01-deployment.ipynb](byom-oss-llm-code/ollama/01-deployment.ipynb)
- [02-ollama.ipynb](byom-oss-llm-code/ollama/02-ollama.ipynb)

### Option 4: Bring open-sourced LLMs into SAP AI Core with vLLM
Please follow the jupyter notebooks below to deploy and test **LocalAI** in SAP AI Core.
- [01-deployment.ipynb](byom-oss-llm-code/ollama/01-deployment.ipynb)
- [02-ollama.ipynb](byom-oss-llm-code/ollama/02-ollama.ipynb)