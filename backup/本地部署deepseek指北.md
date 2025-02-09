最近网上deepseek大火，我说我也讲一讲这个部署吧。

### 准备工作
* 一台电脑（最低配置依据不同模型有差异，请自行调试）
* 可以访问[github](https://github.com/)的网络环境，最好可以访问外网，可以找到我之前免费代理的一篇[文章](https://blog.0071126.xyz/post/mian-fei-jie-dian.html)
* 手和脑子

### 下载Ollama
Ollama官网下载：
[https://ollama.com/download](https://ollama.com/download)
如果是Windows用户，有更换模型存储盘需求的（模型默认下载C盘），在下载前请在系统环境变量中增加`OLLAMA_MODELS=PATH-TO-OLLAMA-MODELS`一项（`PATH-TO-OLLAMA-MODELS`替换为自己的模型路径，没下载任何模型之前新建一个文件夹即可）
×系统环境变量请自行查找修改方法

### 下载并运行模型
Ollama下载之后，就可以下载模型了。模型列表详见：[https://ollama.com/models](https://ollama.com/models)

我们现在进行下载deepseek-r1模型。打开模型列表，找到deepseek-r1这个选项，进入deepseek-r1的页面：[https://ollama.com/library/deepseek-r1](https://ollama.com/library/deepseek-r1)

找到适合自己的模型大小（方法：4G显存以下1.5b(1.5b效果实在不好，不建议本地部署)，8G显存可以流畅跑7b/8b，再之后我没测试了，量力而行）

**注意：ollama上除了671b版本是完整的deepseek-r1，其他都是Qwen/Llama蒸馏(distill)得到的模型，效果不如原版，只有本地部署的优势**

在windows的command prompt（cmd）中，输入`ollama run <model-name>`，其中`<model-name>`替换为需要跑的模型，比如`deepseek-r1:1.5b`
输入后回车，模型会自动开始下载并运行。当出现：

![Image](https://github.com/user-attachments/assets/24b3c8b3-e6ee-4e3d-93ba-927bc1812af6)

这样的提示的时候，就代表部署成功，正在运行了。这时候就可以通过命令行与ai互动了。

### 下载ChatBox获得更好的对话体验
ChatBox仓库：
[https://github.com/Bin-Huang/chatbox](https://github.com/Bin-Huang/chatbox)
根据提示自行下载chatbox，之后在 `设置-模型-模型提供方` 中选择`OLLAMA API`

![Image](https://github.com/user-attachments/assets/2b9e8c57-24db-48c0-a822-573d59bda662)

之后选择下载的模型，新建对话，就可以跟ai互动了。chatbox支持渲染markdown，latex等语法语句，体验比命令行好很多。

这样，本地的deepseek就部署完成了。

ps.如果需要没有审核的deepseek，可以跟我一样选择[https://ollama.com/huihui_ai/deepseek-r1-abliterated](https://ollama.com/huihui_ai/deepseek-r1-abliterated) 这个模型。这个是去除了审核的deepseek。