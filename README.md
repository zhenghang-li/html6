# html6
# Chatbot 自定义元素 README

## 一、项目概述
`Chatbot` 是一个自定义的 HTML 元素，它创建了一个简单的聊天机器人界面，能够与 OpenAI 的 `gpt - 3.5 - turbo` 模型进行交互。用户可以在输入框中输入消息，点击发送按钮后，聊天机器人会将用户消息发送至 OpenAI API，并在聊天窗口中显示用户消息以及机器人的回复。

## 二、功能特点
1. **用户界面友好**：具有简洁直观的聊天窗口和输入区域，方便用户与聊天机器人进行交互。聊天窗口中用户消息和机器人回复采用不同的背景颜色区分，提升可读性。
2. **与 OpenAI API 集成**：通过配置的 API 密钥和基础 URL，能够向 OpenAI 的 `gpt - 3.5 - turbo` 模型发送聊天请求，并处理模型返回的响应。
3. **错误处理**：在请求过程中，如果发生 HTTP 错误或其他异常，会在聊天窗口中显示相应的错误提示，告知用户请求失败的情况。

## 三、使用方法
1. **引入自定义元素**：在 HTML 文件中，确保在使用 `chat - bot` 元素之前，已经引入了包含该自定义元素定义的 JavaScript 文件。例如：
```html
<script src="chatbot.js"></script>
```
2. **使用自定义元素**：在 HTML 页面的合适位置直接使用 `<chat - bot>` 标签，如下所示：
```html
<chat - bot></chat - bot>
```
3. **交互操作**：在浏览器中打开包含 `<chat - bot>` 元素的页面后，用户可以在输入框中输入文本消息，然后点击“发送”按钮。用户输入的消息会显示在聊天窗口左侧，机器人的回复会显示在聊天窗口右侧。

## 四、项目结构
1. **HTML 结构**：在 `connectedCallback` 方法中，通过设置 `shadowRoot.innerHTML` 来定义聊天机器人的 HTML 结构，包括一个用于显示聊天记录的 `<div id="chat - window"></div>`、一个输入框 `<input type="text" placeholder="输入消息">` 和一个发送按钮 `<button>发送</button>`。
2. **CSS 样式**：同样在 `connectedCallback` 方法中，通过 `<style>` 标签定义了聊天机器人的样式，包括聊天窗口、消息气泡、输入框和按钮的样式，实现了美观的用户界面设计。
3. **JavaScript 逻辑**：
    - **构造函数 `constructor`**：初始化自定义元素，创建影子 DOM（Shadow DOM）并设置其模式为 `open`。同时定义了用于存储目标数字（`this.targetNumber`，目前未使用）、OpenAI API 密钥（`this.apiKey`）和基础 URL（`this.baseUrl`）的属性。
    - **`connectedCallback` 方法**：在元素插入到文档后执行，负责设置元素的 HTML 结构和样式，并为发送按钮添加点击事件监听器，关联到 `handleMessage` 方法。
    - **`handleMessage` 方法**：获取用户在输入框中输入的消息，去除首尾空格后，如果消息不为空，则创建一个包含用户消息的 `<div>` 元素并添加到聊天窗口中，然后调用 `sendRequestToOpenAI` 方法向 OpenAI API 发送请求，并清空输入框内容。
    - **`sendRequestToOpenAI` 方法**：构建向 OpenAI API 发送请求的数据，包括指定模型为 `gpt - 3.5 - turbo` 和消息数组（包含系统指令和用户消息）。使用 `fetch` 方法发送 POST 请求，处理响应结果。如果请求成功，将机器人的回复显示在聊天窗口中；如果请求失败，在聊天窗口中显示错误提示。
    - **`customElements.define('chat - bot', Chatbot);`**：注册 `Chatbot` 类为自定义元素，名称为 `chat - bot`，使得在 HTML 中可以使用该自定义元素。

## 五、配置说明
1. **API 密钥**：在 `Chatbot` 类的构造函数中，`this.apiKey` 属性存储了 OpenAI API 密钥。
2. **基础 URL**：`this.baseUrl` 属性定义了 API 请求的基础 URL，当前设置为 `'https://api.chatanywhere.tech/v1'`。如果需要使用其他 API 服务或者更改 API 版本，需要相应修改该 URL。

## 六、注意事项
1. **API 密钥安全**：务必妥善保管你的 OpenAI API 密钥，不要将其泄露在公开的代码仓库或不安全的环境中，以免造成安全风险和不必要的费用支出。
2. **网络请求限制**：OpenAI API 可能存在请求频率限制等规则，请确保你的使用符合 OpenAI 的相关政策，避免因频繁请求导致账号受限。
3. **兼容性**：该自定义元素使用了现代 JavaScript 特性和 Web API，如 `fetch`、自定义元素和 Shadow DOM 等。在一些较旧的浏览器中可能无法正常工作，请根据实际需求进行兼容性处理，例如使用 polyfill 来支持旧浏览器。 
