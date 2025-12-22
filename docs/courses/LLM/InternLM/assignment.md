---
icon: fontawesome/solid/pen
comments: true
hide:
  - navigation
---

# Assignments

## L2 轻松玩转书生·浦语大模型趣味 Demo

[笔记地址](./lecture.md/#l2-demo)

### 环境配置

??? note "Config [vimrc](https://github.com/linkch0/vimrc)"

    1. Clone this repo, and install [vim-plug](https://github.com/junegunn/vim-plug):
    
        ```shell
        git clone https://github.com/linkch0/vimrc.git ~/.vimrcs
        curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
            https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
        ```
    
    2. Edit and paste in `~/.vimrc`:
    
        ```
        set runtimepath+=~/.vimrcs
        source ~/.vimrcs/plugin.vim
        source ~/.vimrcs/basic.vim
        source ~/.vimrcs/map.vim
        ```
    
    3. Install plugins in vim:
    
        ```
        :PlugInstall
        :source ~/.vimrc
        ```

??? note "Config zsh"

    1.   Install zsh and tmux:
    
         `apt install -y zsh tmux`
    
         `chsh -s $(which zsh)`
    
    2.   Install [oh-my-zsh](https://ohmyz.sh/):
    
         `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
    
    3.   Install [powerlevel10k](https://github.com/romkatv/powerlevel10k):
    
         -   Clone the repository:
    
             `git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`
    
         -   Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`
    
         -   Restart terminal to config p10k.
    
    4.   Install [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions):
    
         -   Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`):
    
             `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`
    
         -   Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):
    
             ```plaintext
             plugins=( 
                 # other plugins...
                 zsh-autosuggestions
             )
             ```
    
         -   Start a new terminal session.
    
    5.   [Optional] Set vi-mode plugin in `~/.zshrc` and restart terminal:
    
         ```plaintext
         plugins=( 
             # other plugins...
             vi-mode
         )
         ```

### 基础作业

-   [x] InternLM-Chat-7B 模型生成 300 字的小故事

!!! info

    1. 仓库地址：<https://github.com/internlm/InternLM>
    2. 基于 commit `aaaf4d7b0eef8a44d308806381f38a8bbd6e27de`
    3. `cli_demo.py` [tutorial 代码地址](https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md#24-%E7%BB%88%E7%AB%AF%E8%BF%90%E8%A1%8C)

1.   Command Line Demo

     ```python linenums="1" title="cli_demo.py"
     import torch
     from transformers import AutoTokenizer, AutoModelForCausalLM
     
     
     model_name_or_path = "/root/model/Shanghai_AI_Laboratory/internlm-chat-7b"
     
     tokenizer = AutoTokenizer.from_pretrained(model_name_or_path, trust_remote_code=True)
     model = AutoModelForCausalLM.from_pretrained(model_name_or_path, trust_remote_code=True, torch_dtype=torch.bfloat16, device_map='auto')
     model = model.eval()
     
     system_prompt = """You are an AI assistant whose name is InternLM (书生·浦语).
     - InternLM (书生·浦语) is a conversational language model that is developed by Shanghai AI Laboratory (上海人工智能实验室). It is designed to be helpful, honest, and harmless.
     - InternLM (书生·浦语) can understand and communicate fluently in the language chosen by the user such as English and 中文.
     """
     
     messages = [(system_prompt, '')]
     
     print("=============Welcome to InternLM chatbot, type 'exit' to exit.=============")
     
     while True:
         input_text = input("User  >>> ")
         input_text = input_text.replace(' ', '')
         if input_text == "exit":
             break
         response, history = model.chat(tokenizer, input_text, history=messages)
         messages.append((input_text, response))
         print(f"robot >>> {response}")
     ```

     运行效果：

     ![Cli Demo](https://s2.loli.net/2024/01/12/OJUmYrQfcl3PWL8.webp)

2.   Streamlit Web Demo:
     -   将 `web_demo.py` 中的模型路径修改为本地路径，`git diff`:

         ```diff
         diff --git a/web_demo.py b/web_demo.py
         index 26de0ba..7105d63 100644
         --- a/web_demo.py
         +++ b/web_demo.py
         @@ -26,11 +26,11 @@ def on_btn_click():
          @st.cache_resource
          def load_model():
              model = (
         -        AutoModelForCausalLM.from_pretrained("internlm/internlm-chat-7b", trust_remote_code=True)
         +        AutoModelForCausalLM.from_pretrained("/root/model/Shanghai_AI_Laboratory/internlm-chat-7b", trust_remote_code=True)
                  .to(torch.bfloat16)
                  .cuda()
              )
         -    tokenizer = AutoTokenizer.from_pretrained("internlm/internlm-chat-7b", trust_remote_code=True)
         +    tokenizer = AutoTokenizer.from_pretrained("/root/model/Shanghai_AI_Laboratory/internlm-chat-7b", trust_remote_code=True)
              return model, tokenizer
         
         ```

     -   运行：`streamlit run web_demo.py --server.address 127.0.0.1 --server.port 6006`

     -   端口映射：`ssh -CNg -L 6006:127.0.0.1:6006 intern -F ~/.ssh/ssh_config`

     -   Prompt：`请编写一个300字的小故事，描述你作为一个语言模型是如何被训练的。`

     ![Web Demo](https://s2.loli.net/2024/01/12/7FDepucOmUlWRBi.webp)

-   [x] 熟悉 hugging face 下载功能

使用 `huggingface_hub` python 包，下载 `InternLM-20B` 的 config.json 文件到本地

1.   安装依赖：`pip install -U huggingface_hub`

2.   设置[镜像](https://hf-mirror.com/)：`export HF_ENDPOINT=https://hf-mirror.com`

3.   下载代码：

     ```python
     import os 
     from huggingface_hub import hf_hub_download  # Load model directly 
     
     hf_hub_download(repo_id="internlm/internlm-20b", filename="config.json")
     ```

4.   查看 ``config.json` 内容：

     ![config.json](https://s2.loli.net/2024/01/13/1uBinS7K2DHf6Ib.webp)

### 进阶作业

-   [x] 浦语·灵笔的图文理解及创作

!!! info

    1. 代码仓库：<https://github.com/InternLM/InternLM-XComposer>
    2. 基于 commit `2b14928110b6c37c6be2ebaf1ec7e669c6e85b61`

1.   图文创作：

     -   Command

         ```shell
         python examples/web_demo.py  \
             --folder /root/model/Shanghai_AI_Laboratory/internlm-xcomposer-7b \
             --num_gpus 1 \
             --port 6006
         ```

     -   Prompt: `请简要介绍一下香港大学，包含Main Building和Centennial Campus。`

     ![Interleave text image](https://s2.loli.net/2024/01/13/TFHg1d3m5rO24ot.webp)

2.   图片理解：

     ![Multimodal Chat](https://s2.loli.net/2024/01/13/xRYJHUVBKyMSq79.webp)
     
-   [x] Lagent 智能体工具调用

!!! info

    1. 代码仓库：<https://github.com/InternLM/lagent>
    2. 基于 commit `987618c978bd389e2f9e505b4553886f345dc76c`
    3. `recat_web_demo.py` [tutorial 代码地址](https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md#34-%E4%BF%AE%E6%94%B9%E4%BB%A3%E7%A0%81)


输入数学问题，`InternLM-Chat-7B` 模型理解题意生成解此题的 `Python` 代码，`Lagent` 调度送入 `Python` 代码解释器求出该问题的解。

:material-bug: **Bug1**

1.   删掉代码里出现的 `GoogleSearch` ，否则会出现 `ValueError: Please set Serper API key either in the environment as SERPER_API_KEY or pass it as api_key parameter.`

2.   Traceback

     ```plaintext
       File "/root/code/lagent/examples/react_web_demo.py", line 20, in init_state
         action_list = [PythonInterpreter(), GoogleSearch()]
     ```

3.   修改代码第7、20、92行，并把模型路径修改为本地路径，`git diff`:

     ```diff title="react_web_demo.py"
     diff --git a/examples/react_web_demo.py b/examples/react_web_demo.py
     index da6c649..fff29df 100644
     --- a/examples/react_web_demo.py
     +++ b/examples/react_web_demo.py
     @@ -4,7 +4,7 @@ import os
      import streamlit as st
      from streamlit.logger import get_logger
     
     -from lagent.actions import ActionExecutor, GoogleSearch, PythonInterpreter
     +from lagent.actions import ActionExecutor, PythonInterpreter
      from lagent.agents.react import ReAct
      from lagent.llms import GPTAPI
      from lagent.llms.huggingface import HFTransformerCasualLM
     @@ -17,7 +17,7 @@ class SessionState:
              st.session_state['assistant'] = []
              st.session_state['user'] = []
     
     -        action_list = [PythonInterpreter(), GoogleSearch()]
     +        action_list = [PythonInterpreter()]
              st.session_state['plugin_map'] = {
                  action.name: action
                  for action in action_list
     @@ -89,7 +89,7 @@ class StreamlitUI:
                          model_type=option)
                  else:
                      st.session_state['model_map'][option] = HFTransformerCasualLM(
     -                    'internlm/internlm-chat-7b-v1_1')
     +                    '/root/model/Shanghai_AI_Laboratory/internlm-chat-7b')
              return st.session_state['model_map'][option]
     
          def initialize_chatbot(self, model, plugin_action):
     ```

:material-bug: **Bug2**

1.   确保 streamlit 版本在`1.26.0`以上，[tutorial](https://github.com/InternLM/tutorial/blob/main/helloworld/hello_world.md) 中安装的是`1.24.0`，否则会出现 `TypeError: HeadingMixin.header() got an unexpected keyword argument 'divider'` 的错误
2.   Traceback

    ```plaintext
      File "/root/code/lagent/examples/react_web_demo.py", line 50, in init_streamlit
        st.header(':robot_face: :blue[Lagent] Web Demo ', divider='rainbow')
    ```

3.   查看版本：`pip list | grep streamlit`

4.   升级：`pip install --upgrade streamlit`

:material-play-circle: **运行**

1.   `streamlit run ./examples/react_web_demo.py --server.address 127.0.0.1 --server.port 6006`

2.   Prompt：`生成一个一元二次方程，并求解。`

3.   方程 $x^2-2x-4=0$，执行结果：$x=1 \pm \sqrt{5}$

     ![Lagent Demo](https://s2.loli.net/2024/01/13/YK6zWwpjdPbuGcs.webp)

## L3 基于 InternLM 和 Langchain 搭建你的知识库

[笔记地址](./lecture.md/#l3-internlm-langchain)

### 构建向量数据库

```python title="create_db.py" linenums="1"
# 首先导入所需第三方库
from langchain.document_loaders import UnstructuredFileLoader
from langchain.document_loaders import UnstructuredMarkdownLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.vectorstores import Chroma
from langchain.embeddings.huggingface import HuggingFaceEmbeddings
from tqdm import tqdm
import os

# 获取文件路径函数
def get_files(dir_path):
    # args：dir_path，目标文件夹路径
    file_list = []
    for filepath, dirnames, filenames in os.walk(dir_path):
        # os.walk 函数将递归遍历指定文件夹
        for filename in filenames:
            # 通过后缀名判断文件类型是否满足要求
            if filename.endswith(".md"):
                # 如果满足要求，将其绝对路径加入到结果列表
                file_list.append(os.path.join(filepath, filename))
            elif filename.endswith(".txt"):
                file_list.append(os.path.join(filepath, filename))
    return file_list

# 加载文件函数
def get_text(dir_path):
    # args：dir_path，目标文件夹路径
    # 首先调用上文定义的函数得到目标文件路径列表
    file_lst = get_files(dir_path)
    # docs 存放加载之后的纯文本对象
    docs = []
    # 遍历所有目标文件
    for one_file in tqdm(file_lst):
        file_type = one_file.split('.')[-1]
        if file_type == 'md':
            loader = UnstructuredMarkdownLoader(one_file)
        elif file_type == 'txt':
            loader = UnstructuredFileLoader(one_file)
        else:
            # 如果是不符合条件的文件，直接跳过
            continue
        docs.extend(loader.load())
    return docs

# 目标文件夹
tar_dir = [
    "/root/data/InternLM",
    "/root/data/InternLM-XComposer",
    "/root/data/lagent",
    "/root/data/lmdeploy",
    "/root/data/opencompass",
    "/root/data/xtuner"
]

# 加载目标文件
docs = []
for dir_path in tar_dir:
    docs.extend(get_text(dir_path))

# 对文本进行分块
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500, chunk_overlap=150)
split_docs = text_splitter.split_documents(docs)

# 加载开源词向量模型
embeddings = HuggingFaceEmbeddings(model_name="/root/data/model/sentence-transformer")

# 构建向量数据库
# 定义持久化路径
persist_directory = 'data_base/vector_db/chroma'
# 加载数据库
vectordb = Chroma.from_documents(
    documents=split_docs,
    embedding=embeddings,
    persist_directory=persist_directory  # 允许我们将persist_directory目录保存到磁盘上
)
# 将加载的向量数据库持久化到磁盘上
vectordb.persist()
```

运行截图：

![构建向量数据库](https://s2.loli.net/2024/01/21/y4HenjmwlLMgrID.webp)

### InternLM 接入 LangChain

```python title="LLM.py" linenums="1"
from langchain.llms.base import LLM
from typing import Any, List, Optional
from langchain.callbacks.manager import CallbackManagerForLLMRun
from transformers import AutoTokenizer, AutoModelForCausalLM
import torch

class InternLM_LLM(LLM):
    # 基于本地 InternLM 自定义 LLM 类
    tokenizer : AutoTokenizer = None
    model: AutoModelForCausalLM = None

    def __init__(self, model_path :str):
        # model_path: InternLM 模型路径
        # 从本地初始化模型
        super().__init__()
        print("正在从本地加载模型...")
        self.tokenizer = AutoTokenizer.from_pretrained(model_path, trust_remote_code=True)
        self.model = AutoModelForCausalLM.from_pretrained(model_path, trust_remote_code=True).to(torch.bfloat16).cuda()
        self.model = self.model.eval()
        print("完成本地模型的加载")

    def _call(self, prompt : str, stop: Optional[List[str]] = None,
                run_manager: Optional[CallbackManagerForLLMRun] = None,
                **kwargs: Any):
        # 重写调用函数
        system_prompt = """You are an AI assistant whose name is InternLM (书生·浦语).
        - InternLM (书生·浦语) is a conversational language model that is developed by Shanghai AI Laboratory (上海人工智能实验室). It is designed to be helpful, honest, and harmless.
        - InternLM (书生·浦语) can understand and communicate fluently in the language chosen by the user such as English and 中文.
        """
        
        messages = [(system_prompt, '')]
        response, history = self.model.chat(self.tokenizer, prompt , history=messages)
        return response
        
    @property
    def _llm_type(self) -> str:
        return "InternLM"

if __name__ == "__main__":
    # 测试代码
    llm = InternLM_LLM(model_path = "/root/data/model/Shanghai_AI_Laboratory/internlm-chat-7b")
    print(llm.predict("你是谁"))
```

### 构建检索问答链

对比检索问答链和纯 LLM 的问答效果

```python title="compare.py" linenums="1"
from langchain.vectorstores import Chroma
from langchain.embeddings.huggingface import HuggingFaceEmbeddings
from LLM import InternLM_LLM
from langchain.chains import RetrievalQA

# 定义 Embeddings
embeddings = HuggingFaceEmbeddings(model_name="/root/data/model/sentence-transformer")

# 向量数据库持久化路径
persist_directory = 'data_base/vector_db/chroma'

# 加载数据库
vectordb = Chroma(
    persist_directory=persist_directory, 
    embedding_function=embeddings
)

llm = InternLM_LLM(model_path = "/root/data/model/Shanghai_AI_Laboratory/internlm-chat-7b")
qa_chain = RetrievalQA.from_chain_type(llm,retriever=vectordb.as_retriever(),return_source_documents=True,chain_type_kwargs={"prompt":QA_CHAIN_PROMPT})

# 检索问答链回答效果
question = "什么是InternLM"
result = qa_chain({"query": question})
print("检索问答链回答 question 的结果：")
print(result["result"])

# 仅 LLM 回答效果
result_2 = llm(question)
print("大模型回答 question 的结果：")
print(result_2)
```

运行截图：

![对比检索问答链和纯 LLM 的问答效果](https://s2.loli.net/2024/01/21/Xu8I3YUbH7ZFSQc.webp)

### Gradio Web Demo

```python title="run_gradio.py" linenums="1"
# 导入必要的库
import gradio as gr
from langchain.vectorstores import Chroma
from langchain.embeddings.huggingface import HuggingFaceEmbeddings
import os
from LLM import InternLM_LLM
from langchain.prompts import PromptTemplate

def load_chain():
    # 加载问答链
    # 定义 Embeddings
    embeddings = HuggingFaceEmbeddings(model_name="/root/data/model/sentence-transformer")

    # 向量数据库持久化路径
    persist_directory = 'data_base/vector_db/chroma'

    # 加载数据库
    vectordb = Chroma(
        persist_directory=persist_directory,  # 允许我们将persist_directory目录保存到磁盘上
        embedding_function=embeddings
    )

    llm = InternLM_LLM(model_path = "/root/data/model/Shanghai_AI_Laboratory/internlm-chat-7b")

    # 你可以修改这里的 prompt template 来试试不同的问答效果
    template = """请使用以下提供的上下文来回答用户的问题。如果无法从上下文中得到答案，请回答你不知道，并总是使用中文回答。
    提供的上下文：
    ···
    {context}
    ···
    用户的问题: {question}
    你给的回答:"""

    QA_CHAIN_PROMPT = PromptTemplate(input_variables=["context","question"],
                                    template=template)

    # 运行 chain
    from langchain.chains import RetrievalQA

    qa_chain = RetrievalQA.from_chain_type(llm,
                                        retriever=vectordb.as_retriever(),
                                        return_source_documents=True,
                                        chain_type_kwargs={"prompt":QA_CHAIN_PROMPT})
    
    return qa_chain

class Model_center():
    """
    存储问答 Chain 的对象 
    """
    def __init__(self):
        self.chain = load_chain()

    def qa_chain_self_answer(self, question: str, chat_history: list = []):
        """
        调用不带历史记录的问答链进行回答
        """
        if question == None or len(question) < 1:
            return "", chat_history
        try:
            chat_history.append(
                (question, self.chain({"query": question})["result"]))
            return "", chat_history
        except Exception as e:
            return e, chat_history


model_center = Model_center()

block = gr.Blocks()
with block as demo:
    with gr.Row(equal_height=True):   
        with gr.Column(scale=15):
            gr.Markdown("""<h1><center>InternLM</center></h1>
                <center>书生浦语</center>
                """)
        # gr.Image(value=LOGO_PATH, scale=1, min_width=10,show_label=False, show_download_button=False)

    with gr.Row():
        with gr.Column(scale=4):
            chatbot = gr.Chatbot(height=450, show_copy_button=True)
            # 创建一个文本框组件，用于输入 prompt。
            msg = gr.Textbox(label="Prompt/问题")

            with gr.Row():
                # 创建提交按钮。
                db_wo_his_btn = gr.Button("Chat")
            with gr.Row():
                # 创建一个清除按钮，用于清除聊天机器人组件的内容。
                clear = gr.ClearButton(
                    components=[chatbot], value="Clear console")
                
        # 设置按钮的点击事件。当点击时，调用上面定义的 qa_chain_self_answer 函数，并传入用户的消息和聊天历史记录，然后更新文本框和聊天机器人组件。
        db_wo_his_btn.click(model_center.qa_chain_self_answer, inputs=[
                            msg, chatbot], outputs=[msg, chatbot])
        
    gr.Markdown("""提醒：<br>
    1. 初始化数据库时间可能较长，请耐心等待。
    2. 使用中如果出现异常，将会在文本输入框进行展示，请不要惊慌。 <br>
    """)
# threads to consume the request
gr.close_all()
# 启动新的 Gradio 应用，设置分享功能为 True，并使用环境变量 PORT1 指定服务器端口。
# demo.launch(share=True, server_port=int(os.environ['PORT1']))
# 直接启动
demo.launch()
```

运行截图：

![Gradio Web Demo](https://s2.loli.net/2024/01/21/w5tNJz9gOomfQqp.webp)

## L4 XTuner 大模型单卡低成本微调实战

[笔记地址](./lecture.md/#l4-xtuner)

参考答案：<https://github.com/InternLM/tutorial/blob/main/xtuner/self.md>

### 生成数据集

```python title="generate_data.py" linenums="1"
import json

# 输入你的名字
name = 'Link Chen'
# 重复次数
n = 10000

data = [
    {
        "conversation": [
            {
                "input": "请做一下自我介绍",
                "output": "我是{}的小助手，内在是上海AI实验室书生·浦语的7B大模型哦".format(name)
            }
        ]
    }
]

for i in range(n):
    data.append(data[0])

with open('personal_assistant.json', 'w', encoding='utf-8') as f:
    json.dump(data, f, ensure_ascii=False, indent=4)
```

### 修改配置文件

```shell
mkdir /root/personal_assistant/config && cd /root/personal_assistant/config
xtuner copy-cfg internlm_chat_7b_qlora_oasst1_e3 .
```

修改高亮的行

```python title="internlm_chat_7b_qlora_oasst1_e3_copy.py" linenums="1" hl_lines="25 28 30 34 37 50 53 94-95 98-99"
# Copyright (c) OpenMMLab. All rights reserved.
import torch
from datasets import load_dataset
from mmengine.dataset import DefaultSampler
from mmengine.hooks import (CheckpointHook, DistSamplerSeedHook, IterTimerHook,
                            LoggerHook, ParamSchedulerHook)
from mmengine.optim import AmpOptimWrapper, CosineAnnealingLR, LinearLR
from peft import LoraConfig
from torch.optim import AdamW
from transformers import (AutoModelForCausalLM, AutoTokenizer,
                          BitsAndBytesConfig)

from xtuner.dataset import process_hf_dataset
from xtuner.dataset.collate_fns import default_collate_fn
from xtuner.dataset.map_fns import oasst1_map_fn, template_map_fn_factory
from xtuner.engine.hooks import DatasetInfoHook, EvaluateChatHook
from xtuner.engine.runner import TrainLoop
from xtuner.model import SupervisedFinetune
from xtuner.utils import PROMPT_TEMPLATE

#######################################################################
#                          PART 1  Settings                           #
#######################################################################
# Model
pretrained_model_name_or_path = '/root/data/model/Shanghai_AI_Laboratory/internlm-chat-7b'

# Data
data_path = '/root/personal_assistant/data/personal_assistant.json'
prompt_template = PROMPT_TEMPLATE.internlm_chat
max_length = 512
pack_to_max_length = True

# Scheduler & Optimizer
batch_size = 2  # per_device
accumulative_counts = 16
dataloader_num_workers = 0
max_epochs = 3
optim_type = AdamW
lr = 2e-4
betas = (0.9, 0.999)
weight_decay = 0
max_norm = 1  # grad clip
warmup_ratio = 0.03

# Save
save_steps = 500
save_total_limit = 2  # Maximum checkpoints to keep (-1 means unlimited)

# Evaluate the generation performance during the training
evaluation_freq = 90
SYSTEM = ''
evaluation_inputs = [
    '请介绍一下你自己', '请做一下自我介绍'
]

#######################################################################
#                      PART 2  Model & Tokenizer                      #
#######################################################################
tokenizer = dict(
    type=AutoTokenizer.from_pretrained,
    pretrained_model_name_or_path=pretrained_model_name_or_path,
    trust_remote_code=True,
    padding_side='right')

model = dict(
    type=SupervisedFinetune,
    llm=dict(
        type=AutoModelForCausalLM.from_pretrained,
        pretrained_model_name_or_path=pretrained_model_name_or_path,
        trust_remote_code=True,
        torch_dtype=torch.float16,
        quantization_config=dict(
            type=BitsAndBytesConfig,
            load_in_4bit=True,
            load_in_8bit=False,
            llm_int8_threshold=6.0,
            llm_int8_has_fp16_weight=False,
            bnb_4bit_compute_dtype=torch.float16,
            bnb_4bit_use_double_quant=True,
            bnb_4bit_quant_type='nf4')),
    lora=dict(
        type=LoraConfig,
        r=64,
        lora_alpha=16,
        lora_dropout=0.1,
        bias='none',
        task_type='CAUSAL_LM'))

#######################################################################
#                      PART 3  Dataset & Dataloader                   #
#######################################################################
train_dataset = dict(
    type=process_hf_dataset,
    #  dataset=dict(type=load_dataset, path=data_path),
    dataset=dict(type=load_dataset, path='json', data_files=dict(train=data_path)),
    tokenizer=tokenizer,
    max_length=max_length,
    #  dataset_map_fn=oasst1_map_fn,
    dataset_map_fn=None,
    template_map_fn=dict(
        type=template_map_fn_factory, template=prompt_template),
    remove_unused_columns=True,
    shuffle_before_pack=True,
    pack_to_max_length=pack_to_max_length)

train_dataloader = dict(
    batch_size=batch_size,
    num_workers=dataloader_num_workers,
    dataset=train_dataset,
    sampler=dict(type=DefaultSampler, shuffle=True),
    collate_fn=dict(type=default_collate_fn))

#######################################################################
#                    PART 4  Scheduler & Optimizer                    #
#######################################################################
# optimizer
optim_wrapper = dict(
    type=AmpOptimWrapper,
    optimizer=dict(
        type=optim_type, lr=lr, betas=betas, weight_decay=weight_decay),
    clip_grad=dict(max_norm=max_norm, error_if_nonfinite=False),
    accumulative_counts=accumulative_counts,
    loss_scale='dynamic',
    dtype='float16')

# learning policy
# More information: https://github.com/open-mmlab/mmengine/blob/main/docs/en/tutorials/param_scheduler.md  # noqa: E501
param_scheduler = [
    dict(
        type=LinearLR,
        start_factor=1e-5,
        by_epoch=True,
        begin=0,
        end=warmup_ratio * max_epochs,
        convert_to_iter_based=True),
    dict(
        type=CosineAnnealingLR,
        eta_min=0.0,
        by_epoch=True,
        begin=warmup_ratio * max_epochs,
        T_max=max_epochs,
        convert_to_iter_based=True)
]

# train, val, test setting
train_cfg = dict(type=TrainLoop, max_epochs=max_epochs)

#######################################################################
#                           PART 5  Runtime                           #
#######################################################################
# Log the dialogue periodically during the training process, optional
custom_hooks = [
    dict(type=DatasetInfoHook, tokenizer=tokenizer),
    dict(
        type=EvaluateChatHook,
        tokenizer=tokenizer,
        every_n_iters=evaluation_freq,
        evaluation_inputs=evaluation_inputs,
        system=SYSTEM,
        prompt_template=prompt_template)
]

# configure default hooks
default_hooks = dict(
    # record the time of every iteration.
    timer=dict(type=IterTimerHook),
    # print log every 10 iterations.
    logger=dict(type=LoggerHook, log_metric_by_epoch=False, interval=10),
    # enable the parameter scheduler.
    param_scheduler=dict(type=ParamSchedulerHook),
    # save checkpoint per `save_steps`.
    checkpoint=dict(
        type=CheckpointHook,
        by_epoch=False,
        interval=save_steps,
        max_keep_ckpts=save_total_limit),
    # set sampler seed in distributed evrionment.
    sampler_seed=dict(type=DistSamplerSeedHook),
)

# configure environment
env_cfg = dict(
    # whether to enable cudnn benchmark
    cudnn_benchmark=False,
    # set multi process parameters
    mp_cfg=dict(mp_start_method='fork', opencv_num_threads=0),
    # set distributed parameters
    dist_cfg=dict(backend='nccl'),
)

# set visualizer
visualizer = None

# set log level
log_level = 'INFO'

# load from which checkpoint
load_from = None

# whether to resume training from the loaded checkpoint
resume = False

# Defaults to use random seed and disable `deterministic`
randomness = dict(seed=None, deterministic=False)

# set log processor
log_processor = dict(by_epoch=False)
```

### 训练并保存模型参数

-   Before training

    ![Before training](https://s2.loli.net/2024/01/27/M25iqdvNPmZgyxf.webp)

-   After training

    ![After training](https://s2.loli.net/2024/01/27/M6xnXFh8Ws1wYcv.webp)

-   训练完成

    ![训练完成](https://s2.loli.net/2024/01/27/AtBFhX3DSsz64Qa.webp)

微调后参数转换/合并：

1.   训练后的 pth 格式参数转 Hugging Face 格式

     ```shell
     # 创建用于存放Hugging Face格式参数的hf文件夹
     mkdir /root/personal_assistant/config/work_dirs/hf
     
     export MKL_SERVICE_FORCE_INTEL=1
     
     # 配置文件存放的位置
     export CONFIG_NAME_OR_PATH=/root/personal_assistant/config/internlm_chat_7b_qlora_oasst1_e3_copy.py
     
     # 模型训练后得到的pth格式参数存放的位置
     export PTH=/root/personal_assistant/config/work_dirs/internlm_chat_7b_qlora_oasst1_e3_copy/iter_1152.pth
     
     # pth文件转换为Hugging Face格式后参数存放的位置
     export SAVE_PATH=/root/personal_assistant/config/work_dirs/hf
     
     # 执行参数转换
     xtuner convert pth_to_hf $CONFIG_NAME_OR_PATH $PTH $SAVE_PATH
     ```

     ![转化 pth 为 HF 格式](https://s2.loli.net/2024/01/27/EXyRiSmcQGVlrxI.webp)

     ```shell
     ❯ ls /root/personal_assistant/config/work_dirs/hf
     README.md  adapter_config.json  adapter_model.bin  xtuner_config.py
     ```

2.   Merge 模型参数

     ```shell
     export MKL_SERVICE_FORCE_INTEL=1
     export MKL_THREADING_LAYER='GNU'
     
     # 原始模型参数存放的位置
     export NAME_OR_PATH_TO_LLM=/root/data/model/Shanghai_AI_Laboratory/internlm-chat-7b
     
     # Hugging Face格式参数存放的位置
     export NAME_OR_PATH_TO_ADAPTER=/root/personal_assistant/config/work_dirs/hf
     
     # 最终Merge后的参数存放的位置
     mkdir /root/personal_assistant/config/work_dirs/hf_merge
     export SAVE_PATH=/root/personal_assistant/config/work_dirs/hf_merge
     
     # 执行参数Merge
     xtuner convert merge \
         $NAME_OR_PATH_TO_LLM \
         $NAME_OR_PATH_TO_ADAPTER \
         $SAVE_PATH \
         --max-shard-size 2GB
     ```

     ![Merge 参数](https://s2.loli.net/2024/01/27/P3KQpOWCtGlEs8n.webp)

     ```shell
     ❯ ls /root/personal_assistant/config/work_dirs/hf_merge
     config.json                       pytorch_model-00002-of-00008.bin  pytorch_model-00007-of-00008.bin  tokenizer.model
     configuration_internlm.py         pytorch_model-00003-of-00008.bin  pytorch_model-00008-of-00008.bin  tokenizer_config.json
     generation_config.json            pytorch_model-00004-of-00008.bin  pytorch_model.bin.index.json
     modeling_internlm.py              pytorch_model-00005-of-00008.bin  special_tokens_map.json
     pytorch_model-00001-of-00008.bin  pytorch_model-00006-of-00008.bin  tokenization_internlm.py
     ```

### Gradio Web Demo

-   Before training

    ![Before training Web](https://s2.loli.net/2024/01/27/DQ7xUpnk8GFtzWc.webp)

-   After training

    ![After training Web](https://s2.loli.net/2024/01/27/oD3icXJNwfR4zMS.webp)

## L5 LMDeploy 大模型量化部署实践

[笔记地址](./lecture.md/#l5-lmdeploy)

## L6 OpenCompass 大模型评测解读及实战指南

[笔记地址](./lecture.md/#l6-opencompass)
