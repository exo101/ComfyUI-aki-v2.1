# ComfyUI 使用说明

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
  - checkpoints/ - 大型模型检查点文件
  - loras/ - LoRA微调模型
  - vae/ - 变分自编码器模型
  - clip/ - CLIP文本编码器模型
  - controlnet/ - ControlNet模型
  - upscale_models/ - 超分辨率模型
  - embeddings/ - 文本嵌入模型
  - 等等...

### 应用程序相关

- [nodes.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/nodes.py) - 内置节点的实现，包括文本编码、条件组合、采样等核心功能
- [main.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/main.py) - 程序入口文件，负责初始化环境和启动服务
- [server.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/server.py) - Web服务器实现，处理前端请求和WebSocket通信
- [web/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/web) - 前端界面文件
- [execution.py](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/execution.py) - 工作流执行逻辑

### 其他重要文件

- [requirements.txt](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/requirements.txt) - Python依赖包列表
- [README.md](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/README.md) - 项目说明文档
- [extra_model_paths.yaml.example](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/extra_model_paths.yaml.example) - 模型路径配置示例文件

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

## 运行ComfyUI

要在本地运行ComfyUI，请按照以下步骤操作：

1. 确保已安装Python 3.10或更高版本
2. 安装依赖包：`pip install -r requirements.txt`
3. 将模型文件放置到对应的[models/](file:///d%3A/ComfyUI-aki-v2.0/ComfyUI/models)子目录中
4. 运行命令：`python main.py`
5. 在浏览器中打开 `http://127.0.0.1:8188`

您也可以使用Windows便携版，下载解压后直接运行即可。

## 总结

ComfyUI 通过其独特的节点式界面，为用户提供了一种灵活且强大的方式来创建复杂的AI图像生成工作流。其模块化的设计使得用户可以根据需要自由组合各种功能节点，实现个性化的创作需求。通过熟悉目录结构和界面布局，您可以更好地利用这个工具进行AI艺术创作。
