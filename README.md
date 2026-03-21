# ComfyUI 
<img width="1917" height="1030" alt="Snipaste_2025-10-13_18-28-53" src="https://github.com/user-attachments/assets/8f182bd1-a929-49d6-92cb-9ad25e1beec3" />

## 版本环境：
- python3.11.9  
- CUDA130+torch2.91
- triton-windows=3.5.1.post24
- sageattention=2.2.0
- flash_attn=2.8.3
- nunchaku=1.21
- diffusers-0.36.0


ComfyUI 是一个强大且模块化的视觉AI引擎和应用程序，它允许用户通过基于图形/节点/流程图的界面设计和执行高级稳定扩散管线。本文档将介绍ComfyUI的目录结构和用户界面。

此整合包根据秋叶整合包更新环境适应50系显卡，安装了大多数常用节点与插件，包括wan2.2视频生成所需环境
下载地址：个人主页视频简介下方

https://www.bilibili.com/video/BV1BCHXzJE1C/?spm_id_from=333.788.videopod.sections&vd_source=343e49b703fb5b4137cd6c1987846f37

## 目录结构

ComfyUI 的目录结构清晰地划分了不同的功能模块，以下是主要目录和文件的作用说明：

### 核心目录

- [comfy/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/comfy) - 包含核心功能实现，如模型管理、采样器、文本编码等基础组件
- [comfy_extras/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/comfy_extras) - 额外的功能节点，提供更多的模型支持和特殊效果
- [custom_nodes/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/custom_nodes) - 自定义节点插件目录，可以扩展ComfyUI的功能
- [models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models) - 存放各种模型文件，按类型分类存储：
  - [checkpoints/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/checkpoints/) - 完整的大模型文件（如Stable Diffusion模型），这些是图像生成的核心模型
  - [loras/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/loras/) - LoRA（Low-Rank Adaptation）模型，轻量级微调模型，用于给大模型添加特定风格或概念
  - [vae/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/vae/) - 变分自编码器（Variational Autoencoder）模型，用于图像的编码和解码过程
  - [text_encoders/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/text_encoders/) 和 [clip/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/clip/) - CLIP文本编码器模型，用于将文本提示转换为向量表示
  - [controlnet/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/controlnet/) - ControlNet模型，用于控制图像生成的空间结构和姿势等
  - [clip_vision/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/clip_vision/) - CLIP视觉模型，用于处理图像输入并提取视觉特征
  - [diffusion_models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/diffusion_models/) 和 [unet/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/unet/) - 扩散模型的主干网络，通常是UNet架构
  - [upscale_models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/upscale_models/) - 超分辨率模型，用于提升图像质量并将低分辨率图像放大
  - [embeddings/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/embeddings/) - 文本嵌入模型，通常包含特殊的词汇标记或概念
  - [configs/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/configs/) - 模型配置文件，通常是YAML格式，描述模型结构和参数
  - 其他专门用途的目录：
    - [animatediff_models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/animatediff_models/) 和 [animatediff_motion_lora/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/animatediff_motion_lora/) - 用于动画生成的模型
    - [audio_encoders/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/audio_encoders/) - 音频编码器模型
    - [detection/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/detection/) - 图像检测模型
    - [gligen/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/gligen/) - GLIGEN模型（语言引导的图像生成）
    - [hypernetworks/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/hypernetworks/) - 超网络模型
    - [rembg/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/rembg/) - 背景移除模型
    - [sam2/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/sam2/) 和 [sams/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/sams/) - 分割模型（Segment Anything Models）
    - [style_models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/style_models/) - 风格迁移模型
    - [ultralytics/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models/ultralytics/) - Ultralytics YOLO系列目标检测模型

### 应用程序相关

- [nodes.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/nodes.py) - 内置节点的实现，包括文本编码、条件组合、采样等核心功能
- [main.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/main.py) - 程序入口文件，负责初始化环境和启动服务
- [server.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/server.py) - Web服务器实现，处理前端请求和WebSocket通信
- [web/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/web) - 前端界面文件
- [execution.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/execution.py) - 工作流执行逻辑

### 其他重要文件

- [requirements.txt](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/requirements.txt) - Python依赖包列表
- [README.md](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/README.md) - 项目说明文档
- [extra_model_paths.yaml.example](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/extra_model_paths.yaml.) - 模型路径配置示例文件

## UI界面介绍

ComfyUI 提供了一个直观的Web界面，用户可以通过浏览器访问。默认情况下，在启动ComfyUI后可通过 `http://127.0.0.1:8188` 访问。

### 主要界面元素

1. **节点画布区域**
   - 这是主要的工作区域，用于添加、连接和排列节点
   - 可以通过鼠标拖拽移动画布，滚轮缩放视图
   - 双击空白处可打开节点快速搜索面板

2. **节点库面板**
   - 位于左侧，显示所有可用的节点类别
   - 展开每个类别可以看到具体的节点
   - 点击节点可将其添加到画布中

3. **属性面板**
   - 选择节点后，右侧会显示该节点的参数设置
   - 可以在此调整节点的各种参数值

4. **队列和历史面板**
   - 位于右下角，显示生成队列和历史记录
   - 可以查看当前任务进度和之前生成的结果

5. **菜单栏**
   - 位于顶部，包含文件操作、设置和帮助等功能

### 基本操作

- **添加节点**：双击画布空白处打开搜索框，输入节点名称或在左侧节点库中点击添加
- **连接节点**：将一个节点的输出端口（右侧）拖拽到另一个节点的输入端口（左侧）
- **移动节点**：直接拖拽节点即可移动位置
- **删除节点**：选中节点后按Delete键
- **生成图像**：连接好节点后，点击"Queue Prompt"按钮开始生成

### 快捷键

- Ctrl + Enter：排队当前工作流进行生成
- Ctrl + S：保存工作流
- Ctrl + O：加载工作流
- Ctrl + Z/Ctrl + Y：撤销/重做
- Delete：删除选中的节点
- Space：按住空格键并拖动鼠标可移动画布
- Alt + +/-：放大/缩小画布


## 总结

ComfyUI 通过其独特的节点式界面，为用户提供了一种灵活且强大的方式来创建复杂的AI图像生成工作流。其模块化的设计使得用户可以根据需要自由组合各种功能节点，实现个性化的创作需求。通过熟悉目录结构和界面布局，您可以更好地利用这个工具进行AI艺术创作。
