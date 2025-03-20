# html6
# image-box
# quote-box
# PrtSc
# chat-box

# Chatbot 自定义元素 

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
  
 # 网页截图及图片操作功能

## 一、项目概述
该项目实现了在网页中进行屏幕截图，并对截图后的图片提供移动和缩放操作的功能。用户点击“截图”按钮后，能够截取当前屏幕内容，并将截图显示在页面中，随后可以通过鼠标操作对截图进行移动和缩放，以满足对截图进行查看和调整的需求。

## 二、功能特点
1. **屏幕截图**：利用浏览器的 `navigator.mediaDevices.getDisplayMedia` API，用户点击按钮即可轻松截取屏幕画面，无需额外的插件或软件。
2. **图片移动**：通过鼠标拖动操作，用户可以在页面中自由移动截图的位置，方便查看图片的不同区域。
3. **图片缩放**：使用鼠标滚轮，能够对截图进行放大或缩小操作，并且缩放范围被限制在 0.1 到 5 倍之间，避免过度缩放导致图片无法正常查看或显示异常。

## 三、使用方法
1. **加载页面**：在支持相关 API 的现代浏览器中打开包含该功能代码的网页。
2. **截图操作**：找到页面上的“截图”按钮（其 `id` 为 `captureBtn`），点击该按钮。此时浏览器会弹出屏幕共享的权限请求，用户允许后，页面将自动完成屏幕截图，并将截图显示在指定的 `<img id="screenshotImg">` 元素中。
3. **图片移动**：鼠标左键点击截图区域，按住鼠标不放并移动鼠标，截图会跟随鼠标移动，实现图片在页面中的位置调整。
4. **图片缩放**：将鼠标悬停在截图上，滚动鼠标滚轮。向前滚动滚轮放大图片，向后滚动滚轮缩小图片，图片会根据设置的缩放范围进行相应缩放。

## 四、代码结构与原理
1. **事件监听与初始化**：
    - 使用 `document.addEventListener('DOMContentLoaded', function () {})` 确保页面 DOM 加载完成后执行后续代码。
    - 获取页面中的“截图”按钮（`captureBtn`）和用于显示截图的图片元素（`screenshotImg`）。
    - 初始化一些变量，如 `isDragging` 用于跟踪是否正在进行拖动操作，`startX`、`startY` 用于记录鼠标按下时的初始位置，`translateX`、`translateY` 用于记录图片的平移量，`scale` 用于记录图片的缩放比例。
2. **截图功能实现**：
    - 为“截图”按钮添加 `click` 事件监听器。
    - 在事件处理函数中，通过 `navigator.mediaDevices.getDisplayMedia` 获取屏幕的媒体流，该媒体流包含屏幕的视频数据。
    - 创建一个 `<video>` 元素，将获取到的媒体流设置为其 `srcObject`，并将视频元素添加到页面中，设置为隐藏状态。
    - 等待视频播放后，创建一个 `<canvas>` 元素，获取其 2D 绘图上下文 `ctx`。设置 `canvas` 的宽度和高度与视频的宽度和高度一致。
    - 使用 `ctx.drawImage` 将视频内容绘制到 `canvas` 上，然后通过 `canvas.toDataURL('image/png')` 将 `canvas` 内容转换为 PNG 格式的图片数据 URL，并将其设置为 `screenshotImg` 的 `src` 属性，从而实现截图显示。
    - 停止媒体流中的所有轨道，并从页面中移除视频元素。
    - 调用 `initDragAndZoom` 函数初始化图片的移动和缩放功能。
3. **移动和缩放功能实现**：
    - **移动功能**：
        - 在 `initDragAndZoom` 函数中，为 `screenshotImg` 添加 `mousedown` 事件监听器，当鼠标按下时，设置 `isDragging` 为 `true`，并记录鼠标相对于图片当前位置的初始偏移量 `startX` 和 `startY`。
        - 为 `document` 添加 `mousemove` 事件监听器，当鼠标移动且处于拖动状态（`isDragging` 为 `true`）时，根据鼠标当前位置和初始偏移量计算图片的新平移量 `translateX` 和 `translateY`，并调用 `updatePosition` 函数更新图片的 `transform` 样式，实现图片的移动。
        - 为 `document` 添加 `mouseup` 事件监听器，当鼠标松开时，设置 `isDragging` 为 `false`，停止拖动操作。
    - **缩放功能**：
        - 为 `screenshotImg` 添加 `wheel` 事件监听器，当鼠标滚轮滚动时，根据滚轮滚动方向（向上或向下）计算缩放因子 `delta`，更新 `scale` 值。
        - 将 `scale` 值限制在 0.1 到 5 之间，确保缩放比例在合理范围内。
        - 当 `scale` 值发生变化时，调用 `updateScale` 函数更新图片的 `transform` 样式，实现图片的缩放。
    - **样式更新函数**：
        - `updatePosition` 和 `updateScale` 函数功能类似，都是通过设置 `screenshotImg` 的 `transform` 样式，将图片的平移量 `translateX`、`translateY` 和缩放比例 `scale` 应用到图片上，从而实现图片的实时移动和缩放效果。

## 五、注意事项
1. **浏览器兼容性**：该功能依赖于现代浏览器的 `navigator.mediaDevices.getDisplayMedia` API，目前该 API 在部分旧版本浏览器中可能不支持。请确保使用支持该 API 的浏览器，如最新版本的 Chrome、Firefox 等。
2. **权限问题**：截图操作需要获取屏幕共享权限，用户在点击截图按钮后，浏览器会弹出权限请求提示。如果用户拒绝共享屏幕，截图操作将失败，并在控制台输出错误信息。
3. **性能影响**：频繁进行截图、移动和缩放操作可能会对浏览器性能产生一定影响，尤其是在处理高分辨率屏幕截图时。在实际应用中，需根据具体场景和性能要求进行优化。 
# 自定义HTML元素 - ImageBox和QuoteBox README

## 一、项目概述
本项目定义了两个自定义HTML元素：`image-box` 和 `quote-box`，用于在网页中创建具有特定功能的组件。`image-box` 实现了图片轮播的效果，`quote-box` 则展示带有作者和来源信息的引用文本，并在鼠标悬停时呈现特定的视觉效果。

## 二、功能特点
### （一）ImageBox
1. **图片轮播**：`image-box` 元素能够按照设定的时间间隔（默认为3秒）自动切换展示不同的图片。通过在HTML标签中设置 `img-srcs` 属性来指定要展示的图片URL列表，以逗号分隔。
2. **尺寸定制**：支持通过 `width` 和 `height` 属性来自定义图片展示区域的大小。如果未设置这两个属性，图片展示区域的宽度和高度将默认为 `auto`，即根据图片的原始尺寸进行自适应显示。

### （二）QuoteBox
1. **引用文本展示**：`quote-box` 元素用于展示一段引用文本，同时显示该引用的作者和来源信息。作者和来源信息会以特定的格式和样式附加在引用文本之后。
2. **交互效果**：当鼠标悬停在 `quote-box` 元素上时，会触发交互效果。引用文本所在的盒子背景颜色变为 `#f0f0f0`，引用文本的字体大小增加到 `1.2em`；当鼠标移出时，背景颜色恢复为透明，字体大小恢复为 `1em`。

## 三、使用方法
### （一）ImageBox
1. **在HTML中使用**：在HTML文档中，直接使用 `<image-box>` 标签，并按照以下方式设置属性：
```html
<image-box img-srcs="image1.jpg, image2.jpg, image3.jpg" width="400px" height="300px"></image-box>
```
其中，`img-srcs` 属性指定要轮播的图片URL列表，`width` 和 `height` 属性（可选）用于设置图片展示区域的尺寸。

### （二）QuoteBox
1. **在HTML中使用**：在HTML文档中，使用 `<quote-box>` 标签，并设置相应的属性和文本内容：
```html
<quote-box author="Albert Einstein" source="On the Electrodynamics of Moving Bodies">
    The only source of knowledge is experience.
</quote-box>
```
在上述示例中，`author` 属性指定引用的作者，`source` 属性指定引用的来源，标签之间的文本即为引用的内容。

## 四、代码结构与原理
### （一）ImageBox类
1. **构造函数**：在 `ImageBox` 类的构造函数中，调用 `super()` 来继承 `HTMLElement` 的属性和方法，并通过 `this.attachShadow({ mode: 'open' })` 创建一个开放模式的影子DOM，用于封装元素的样式和结构，避免与页面其他部分的样式冲突。
2. **connectedCallback方法**：当 `image-box` 元素被插入到文档中时，该方法被调用。
    - 从元素的 `img-srcs` 属性中获取图片URL列表，并使用 `split(',')` 方法将其分割成数组。
    - 获取 `width` 和 `height` 属性值，如果未设置则使用默认值 `auto`。
    - 创建一个 `<div>` 元素作为图片的容器，并设置其宽度和高度。
    - 创建一个 `<img>` 元素，将图片URL列表中的第一张图片设置为其 `src` 属性，并将该 `<img>` 元素添加到图片容器 `<div>` 中。
    - 将图片容器 `<div>` 添加到影子DOM中。
    - 调用 `switchImages` 函数，开始图片轮播功能。
3. **switchImages函数**：该函数负责实现图片的轮播逻辑。
    - 从 `galleryElement`（即 `image-box` 元素）的 `img-srcs` 属性中获取图片URL列表并分割成数组。
    - 定义一个变量 `currentIndex` 用于记录当前显示的图片索引，初始值为0。
    - 使用 `setInterval` 函数设置一个定时器，每3000毫秒执行一次。
    - 在定时器的回调函数中，将 `currentIndex` 递增并对图片URL列表的长度取模，以确保索引值在合法范围内。
    - 更新 `imgElement`（即 `image-box` 影子DOM中的 `<img>` 元素）的 `src` 属性，显示下一张图片。

### （二）QuoteBox类
1. **构造函数**：与 `ImageBox` 类类似，`QuoteBox` 类的构造函数调用 `super()` 并创建一个开放模式的影子DOM。
2. **connectedCallback方法**：当 `quote-box` 元素被插入到文档中时，该方法被调用。
    - 从元素的 `author` 和 `source` 属性中获取作者和来源信息。
    - 获取元素的文本内容作为引用文本。
    - 创建一个 `<div>` 元素作为引用文本的容器，并设置其边框、内边距和外边距样式。
    - 创建一个 `<p>` 元素用于显示引用文本，并将作者和来源信息以 `<span>` 元素的形式附加在引用文本之后，同时设置相应的字体样式。
    - 将包含引用文本和相关信息的 `<p>` 元素添加到引用文本容器 `<div>` 中。
    - 将引用文本容器 `<div>` 添加到影子DOM中。
    - 调用 `showQuoteEffect` 函数，为 `quote-box` 元素添加鼠标悬停交互效果。
3. **showQuoteEffect函数**：该函数为 `quoteElement`（即 `quote-box` 元素）添加鼠标悬停和移出的事件监听器。
    - 当鼠标悬停在 `quote-box` 元素上时，通过修改影子DOM中 `<div>` 元素的 `backgroundColor` 属性和 `<p>` 元素的 `fontSize` 属性，实现背景颜色改变和字体大小增加的效果。
    - 当鼠标移出 `quote-box` 元素时，将背景颜色和字体大小恢复为初始值。

## 五、注意事项
1. **属性设置**：在使用 `image-box` 和 `quote-box` 元素时，务必正确设置所需的属性。对于 `image-box`，`img-srcs` 属性是必需的，否则将无法展示图片；对于 `quote-box`，`author` 和 `source` 属性应准确设置，以正确展示引用的相关信息。
2. **样式影响**：由于使用了影子DOM，自定义元素内部的样式不会影响到页面其他部分，同时页面其他部分的样式也不会干扰自定义元素。但在设置自定义元素的样式时，应注意与整体页面风格的协调性。
3. **兼容性**：自定义元素和影子DOM的支持程度在不同浏览器中可能存在差异。在使用这些功能时，请确保目标浏览器支持相关的Web标准。对于不支持的浏览器，可以考虑使用polyfill或其他兼容方案来实现类似的功能。 
