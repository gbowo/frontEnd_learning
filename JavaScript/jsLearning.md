``` javascript
const one = "你好，";
const two = "请问最近如何？";
const joined = `${one}${two}`;
console.log(joined); // "你好，请问最近如何？"
```
像这样连接字符串被称为串联（concatenation）


### 字符串方法

**获取长度**：
``` js
let browserType = "mozilla";
browserType.length;
```

**检索特定字符串字符**
``` js
browserType[0];
```

**在字符串中查找子字符串并提取它**
``` js
browserType.indexOf("zilla");
```
结果是 2，因为子字符串“zilla”从“mozilla”内的位置 2（0、1、2——所以从第 3 个字符）开始。这样的代码可以用来过滤字符串。例如，假设我们有一个 Web 地址列表，但我们只想打印出包含“mozilla”的那些地址。

找不到子字符串时返回-1

**根据位置提取子字符串**

``` js
browserType.slice(0, 3);
```

**转换大小写**

``` js
let radData = "My NaMe Is MuD";
radData.toLowerCase();
radData.toUpperCase();
```

**替换字符串的某个部分**

``` js
browserType.replace("moz", "van");
```

### 数组

**字符串和数组之间的转换**

- **将字符串中用逗号隔开的分别装进数组**
```js
let myData = "Manchester,London,Liverpool,Birmingham,Leeds,Carlisle";
let myArray = myData.split(",");
myArray;
```
- **将数组中的元素之间的逗号包含并加入字符串**
``` js
let myNewString = myArray.join(",");
myNewString;
```
join()可以指定不同的分隔符

使用toString()
``` js
let dogNames = ["Rocket", "Flash", "Bella", "Slugger"];
dogNames.toString(); //Rocket,Flash,Bella,Slugger
```


**添加和删除数组项**

**push()**：将元素添加到数组末尾，返回数组的新长度。

**pop()**：从数组中删除最后一个元素，返回已删除的元素。

**unshift()**：将元素添加到数组开始，返回数组新长度

**shift()**：将数组第一个元素删除，返回已删除的元素


### 事件

事件是发生在你正在编程的系统中的事情——当事件发生时，系统产生（或“触发”）某种信号，并提供一种机制，当事件发生时，可以自动采取某种行动（即运行一些代码）。事件是在浏览器窗口内触发的，并倾向于附加到驻留在其中的特定项目。这可能是一个单一的元素，一组元素，当前标签中加载的 HTML 文档，或整个浏览器窗口。有许多不同类型的事件可以发生。

为了对一个事件做出反应，你要给它附加一个**事件处理器**。这是一个代码块（通常是你作为程序员创建的一个 JavaScript 函数），在事件发生时运行。当这样一个代码块被定义为响应一个事件而运行时，我们说我们在**注册一个事件处理器**。注意，事件处理器有时候被叫做**事件监听器**——从我们的用意来看这两个名字是相同的，尽管严格地来说这块代码既监听也处理事件。监听器留意事件是否发生，处理器对事件发生做出回应。


**处理点击事件**

``` js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

btn.addEventListener("click", () => {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
});
```

**使用addEventListener()**

HTML \<button\> 元素将在用户点击按钮时触发一个事件。所以它定义了一个 addEventListener() 函数，我们在这里调用它。我们要传入两个参数：

字符串 "click"，表示我们要监听点击事件。按钮可以触发很多其他的事件，比如当用户将鼠标移到按钮上时（"mouseover" 事件），或者当用户按下一个键并且按钮被聚焦时（"keydown" 事件）。
当事件发生时所调用的函数。在我们的例子中，该函数生成一个随机的 RGB 颜色，并将页面 \<body\> 的 background-color 设置为该颜色。

把处理函数作为一个单独的具名函数也是可以的，像这样：

``` js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function changeBackground() {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
}

btn.addEventListener("click", changeBackground);

```

**监听其他事件**

**focus** 和 **blur**：当按钮被聚焦或失焦时，颜色会改变；尝试按下 **tab** 键来聚焦于按钮，再次按下该键来使按钮失去焦点。这些事件通常用于在聚焦时显示填入表单字段的信息，或者在表单字段填入不正确的值时显示错误信息。
**dblclick**：颜色只在按钮被双击时改变。
**mouseover** 和 **mouseout**：当鼠标指针在按钮上悬停，或指针移出按钮时，颜色分别会改变。


一些事件，如 click（点击事件），几乎对任何元素都可用。其他事件则更具体，只在某些情况下有用：例如，**play** 事件只对某些元素有效，如 \<video\> 元素。


**移除监听器**

如果你使用 addEventListener() 添加了一个事件处理器，你可以使用 removeEventListener() 方法再次删除它。

``` js
btn.removeEventListener("click", changeBackground);
```

事件处理器也可以通过传递 AbortSignal 到 addEventListener()，然后在拥有 AbortSignal 的控制器上调用abort()，从而删除事件处理器。例如，要添加一个可以使用 AbortSignal 来删除的事件处理器，可以这样做：

``` js
const controller = new AbortController();

btn.addEventListener("click",
  () => {
    const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
    document.body.style.backgroundColor = rndCol;
  },
  { signal: controller.signal } // 向该处理器传递 AbortSignal
);
```

然后可以像这样删除上面代码创建的事件处理器：

``` js
controller.abort(); // 移除任何/所有与该控制器相关的事件处理器

```


**事件处理器属性**

可以触发事件的对象（如按钮）通常也有属性，其名称是 on，后面是事件的名称。例如，元素有一个属性 onclick。这被称为事件处理器属性。为了监听事件，你可以将处理函数分配给该属性。

``` js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

btn.onclick = () => {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
};
```
你也可以将处理器属性分配给具名函数：
``` js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

function bgChange() {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
}

btn.onclick = bgChange;
```

对于事件处理器属性，你不能为一个事件添加一个以上的处理程序。

**阻止默认行为**

接下来是 JavaScript 代码——这里我们在 submit 事件（表单提交时触发提交事件）的处理程序中实现一个非常简单的检查，测试文本字段是否为空。如果是这样，我们就在事件对象上调用 preventDefault() 函数，停止表单提交，然后在我们的表单下面的段落中显示错误信息，告诉用户出了什么问题：

``` js
const form = document.querySelector("form");
const fname = document.getElementById("fname");
const lname = document.getElementById("lname");
const para = document.querySelector("p");

form.addEventListener("submit", (e) => {
  if (fname.value === "" || lname.value === "") {
    e.preventDefault();
    para.textContent = "You need to fill in both names!";
  }
});
```

**事件冒泡**

即事件会沿父级方向传递的性质

**stopPropagation()**，event对象的一个函数，用来当在一个事件处理器中调用时防止事件向任何其他元素传递。

``` js
const btn = document.querySelector("button");
const box = document.querySelector("div");
const video = document.querySelector("video");

btn.addEventListener("click", () => box.classList.remove("hidden"));

video.addEventListener("click", (event) => {
  event.stopPropagation();
  video.play();
});

box.addEventListener("click", () => box.classList.add("hidden"));
```


**事件捕获**

与事件冒泡的顺序相反：事件不是先在最内层的目标元素上发生，然后在连续较少的嵌套元素上发生，而是先在最小嵌套元素上发生，然后在连续更多的嵌套元素上发生，直到达到目标。

事件捕获默认是禁用的，你需要在 **addEventListener()** 的 **capture** 选项中启用它。

```html
<body>
  <div id="container">
    <button>点我！</button>
  </div>
  <pre id="output"></pre>
</body>
```

``` js
const output = document.querySelector("#output");
function handleClick(e) {
  output.textContent += `你在 ${e.currentTarget.tagName} 元素上进行了点击\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

document.body.addEventListener("click", handleClick, { capture: true });
container.addEventListener("click", handleClick, { capture: true });
button.addEventListener("click", handleClick);
```


**事件委托**

``` html
<div id="container">
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
  <div class="tile"></div>
</div>
```

``` css
.tile {
  height: 100px;
  width: 25%;
  float: left;
}
```

``` js
function random(number) {
  return Math.floor(Math.random() * number);
}

function bgChange() {
  const rndCol = `rgb(${random(255)}, ${random(255)}, ${random(255)})`;
  return rndCol;
}

const container = document.querySelector("#container");

container.addEventListener("click", (event) => {
  event.target.style.backgroundColor = bgChange();
});
```

在 JavaScript 代码中，我们向每一个区域中添加单击事件处理器。但是，一个更简单、更有效的选择是在父节点上设置点击事件处理器，并依靠事件冒泡来确保用户点击每个区域时处理程序被执行：


### JS对象基础


括号表示法：

另外一种访问对象属性的方式是使用括号表示法（bracket notation），下方所示的点表示法：

```js
person.age;
person.name.first;
```
可以使用如下所示的括号表示法替代：
```js
person["age"];
person["name"]["first"];
```

点表示法通常优于括号表示法，因为它更简洁且更易于阅读。然而，在某些情况下你必须使用括号。例如，如果对象属性名称保存在变量中，则不能使用点表示法访问该值，但可以使用括号表示法访问该值。

```js
const person = {
  name: ["Bob", "Smith"],
  age: 32,
};

function logProperty(propertyName) {
  console.log(person[propertyName]);
}

logProperty("name");
// ["Bob", "Smith"]
logProperty("age");
// 32
```

设置成员并不意味着你只能更新已经存在的属性的值和方法，你也可以创建新的成员。

```js
person["eyes"] = "hazel";
person.farewell = function () {
  console.log("再见！");
};
```

括号表示法一个有用的地方是它不仅可以**动态的去设置对象成员的值**，还可以**动态的去设置成员的名字**。假设我们想让用户能够通过在两个文本输入框中键入成员名称和值，在他们的人员数据中存储自定义的值类型。我们可以像这样获取这些值：

构造函数只是使用 **new** 关键字调用的函数。当你调用构造函数时，它将：
- 创建一个新对象
- 将 this 绑定到新对象，以便你可以在构造函数代码中引用 this
- 运行构造函数中的代码
- 返回新对象

按照惯例，构造函数以大写字母开头，并且以它们创建的对象类型命名。因此，可以将我们的示例重写如下：
``` js
function Person(name) {
  this.name = name;
  this.introduceSelf = function () {
    console.log(`你好！我是 ${this.name}。`);
  };
}
```

要将 Person() 作为构造函数调用，我们使用 new：

```js
const salva = new Person("Salva");
salva.name;
salva.introduceSelf();
// "你好！我是 Salva。"

const frankie = new Person("Frankie");
frankie.name;
frankie.introduceSelf();
// "你好！我是 Frankie。"
```

### DOM脚本简介

Web浏览器的重要部分
- **窗口**（window）是载入网页的浏览器标签；在 JavaScript 中，它由 Window 对象表示。使用这个对象上的方法，你可以做一些事情，比如返回窗口的大小（见 Window.innerWidth 和 Window.innerHeight），操作加载到窗口的文档，在客户端存储该文档的特定数据（例如使用本地数据库或其他存储机制），为当前窗口附加一个事件处理器等。
- **导航器**（navigator）在网络上出现时，代表浏览器的状态和身份（即用户代理）。在 JavaScript 中，它由 Navigator 对象表示。你可以用这个对象来检索用户的首选语言、用户网络摄像头的媒体流等信息。
- **文档**（document，在浏览器中用 DOM 表示）是加载到窗口的实际页面，在 JavaScript 中，它由 Document 对象表示。你可以使用这个对象来返回和操作构成文档的 HTML 和 CSS 的信息，例如，在 DOM 中获得一个元素的引用，改变其文本内容，对其应用新的样式，创建新的元素并将其作为子元素添加到当前元素中，甚至完全删除它。


- 要操作 DOM 内的元素，首先需要选择它，并将它的引用存储在一个变量中。
- 现在我们已经将元素引用存储在一个变量中，我们可以开始使用可用的属性和方法来操作它（它们定义在 \<a\> 元素的 HTMLAnchorElement 接口上，它继承于更一般的父接口 HTMLElement，以及 Node——它代表 DOM 中所有节点）。首先，让我们通过更新 Node.textContent 属性的值来改变链接中的文本。在前一行下面添加以下内容：
- 我们也能修改链接指向的 URL，使得它被点击时不会走向错误的位置。在底部再次加入下列代码：
- 回到当前的例子，我们先获取到 <section> 元素的引用。在已有 script 中添加下列代码（其他代码也同样处理）：
- 现在用 Document.createElement() 创建一个新的段落，用与之前相同的方法赋予相同的文本：
- 现在可以用 Node.appendChild() 方法在后面追加新的段落：
- 最后，在内部链接的段落中添加文本节点，完美的结束句子。首先我们要使用 Document.createTextNode() 创建一个文本节点：
- 现在获取内部连接的段落的引用，并把文本节点附加到这个节点上：
- 也许有时候你想移动或从 DOM 中**删除**节点，这是完全可能的。如果你想把具有内部链接的段落移到 section 的底部，简单的做法是：这样可以把段落下移到 section 的底部。你可能认为它会产生第二个副本，但事实并非如此——linkPara 是对该段落唯一副本的引用。如果你想复制并添加它，你需要使用 Node.cloneNode() 来代替。
- 删除节点也非常的简单，至少，你拥有要删除的节点和其父节点的引用。在当前情况下，我们只要使用 Node.removeChild() 即可，如下：
- 要删除一个**仅基于自身引用**的节点可能稍微有点复杂，这也是很常见的。你可以使用 Element.remove()：
- 此方法在较旧的浏览器中不受支持，它们没有方法告诉一个节点删除自己，所以你必须这样做：

``` js
const link = document.querySelector("a");
link.textContent = "Mozilla Developer Network";
link.href = "https://developer.mozilla.org";
const sect = document.querySelector("section");
const para = document.createElement("p");
para.textContent = "We hope you enjoyed the ride.";
sect.appendChild(para);
const text = document.createTextNode(
  " — the premier source for web development knowledge.",
);
const linkPara = document.querySelector("p");
linkPara.appendChild(text);

para.style.color = "white";
para.style.backgroundColor = "black";
para.style.padding = "10px";
para.style.width = "250px";
para.style.textAlign = "center";

```

```js
sect.appendChild(linkPara);

sect.removeChild(linkPara);

linkPara.remove();

linkPara.parentNode.removeChild(linkPara);

```


**操作样式**

可以使用 Document.stylesheets 来获得一个附加在文档上的所有样式表的列表，它返回一个包含 CSSStyleSheet 对象的类数组。然后你就可以根据需要添加/删除样式了。然而，我们不打算对这些功能进行扩展，因为它们是一种有点过时的、难以操作样式的方式。还有更多更简单的方法。

第一种方法是直接将内联样式添加到你想动态样式的元素上。这是通过 HTMLElement.style 属性实现的，它包含了文档中每个元素的内联样式信息。你可以设置这个对象的属性来直接更新元素样式。

**注意**：CSS 样式的 JavaScript 属性版本是用小驼峰命名法书写的，而 CSS 版本采用连字符（烤串命名法）（例如，backgroundColor 对 background-color）。确保你不要把这些混为一谈，否则将无法工作。

还有一种在文档上动态操作样式的常见方法：在 HTML 的 \<head\> 中添加下列代码 :

``` html
<style>
  .highlight {
    color: white;
    background-color: black;
    padding: 10px;
    width: 250px;
    text-align: center;
  }
</style>
```

现在我们改为使用 HTML 操作的常用方法——Element.setAttribute()——它接受两个参数：想在元素上设置的属性、要为它设置的值。在这种情况下，我们在段落中设置类名为 highlight：

``` js
para.setAttribute("class", "highlight");
```

两种方式各有优缺点，选择哪种取决于你自己。第一种方法需要较少的设置，适合于简单的使用，而第二种方法更纯粹（混合 CSS、JavaScript 和内联样式通常不是一种好的实践，而该方法不会产生这些）。当你开始构建更大和更多的应用程序时，你可能会更多地开始使用第二种方法，但这真的取决于你。


### 异步JavaScript简介

浏览器提供的许多功能（尤其是最有趣的那一部分）可能需要很长的时间来完成，因此需要异步完成，例如：
- 使用 **fetch**() 发起 HTTP 请求
- 使用 **getUserMedia**() 访问用户的摄像头和麦克风
- 使用 **showOpenFilePicker**() 请求用户选择文件以供访问

这就是耗时的同步函数的基本问题。在这里我们想要的是一种方法，以让我们的程序可以：
- 通过调用一个函数来启动一个长期运行的操作
- 让函数开始操作并立即返回，这样我们的程序就可以保持对其他事件做出反应的能力
- 当操作最终完成时，通知我们操作的结果。


一些早期的异步 API 正是以这种方式来使用事件的。**XMLHttpRequest API** 可以让你用 JavaScript 向远程服务器发起 HTTP 请求。由于这样的操作可能需要很长的时间，所以它被设计成异步 API，你可以通过给 XMLHttpRequest 对象附加事件监听器来让程序在请求进展和最终完成时获得通知。

下面的例子展示了这样的操作。点击“点击发起请求”按钮来发送一个请求。我们将创建一个新的 **XMLHttpRequest** 并监听它的 **loadend** 事件。而我们的事件处理程序则会在控制台中输出一个“完成！”的消息和请求的状态代码。

我们在添加了事件监听器后发送请求。注意，在这之后，我们仍然可以在控制台中输出“请求已发起”，也就是说，我们的程序可以在请求进行的同时继续运行，而我们的事件处理程序将在请求完成时被调用。

``` html
<button id="xhr">点击发起请求</button>
<button id="reload">重载</button>

<pre readonly class="event-log"></pre>
```

``` js
const log = document.querySelector(".event-log");
document.querySelector("#xhr").addEventListener("click", () => {
  log.textContent = "";
  const xhr = new XMLHttpRequest();
  xhr.addEventListener("loadend", () => {
    log.textContent = `${log.textContent}完成！状态码：${xhr.status}`;
  });
  xhr.open(
    "GET",
    "https://raw.githubusercontent.com/mdn/content/main/files/en-us/_wikihistory.json",
  );
  xhr.send();
  log.textContent = `${log.textContent}请求已发起\n`;
});
document.querySelector("#reload").addEventListener("click", () => {
  log.textContent = "";
  document.location.reload();
});
```

**回调**

事件处理程序是一种特殊类型的回调函数。而回调函数则是一个被传递到另一个函数中的会在适当的时候被调用的函数。正如我们刚刚所看到的：回调函数曾经是 JavaScript 中实现异步函数的主要方式。

然而，当回调函数本身需要调用其他同样接受回调函数的函数时，基于回调的代码会变得难以理解。当你需要执行一些分解成一系列异步函数的操作时，这将变得十分常见。例如下面这种情况：

``` js
function doStep1(init) {
  return init + 1;
}
function doStep2(init) {
  return init + 2;
}
function doStep3(init) {
  return init + 3;
}
function doOperation() {
  let result = 0;
  result = doStep1(result);
  result = doStep2(result);
  result = doStep3(result);
  console.log(`结果：${result}`);
}
doOperation();
```

使用回调后：

``` js
function doStep1(init, callback) {
  const result = init + 1;
  callback(result);
}
function doStep2(init, callback) {
  const result = init + 2;
  callback(result);
}
function doStep3(init, callback) {
  const result = init + 3;
  callback(result);
}
function doOperation() {
  doStep1(0, (result1) => {
    doStep2(result1, (result2) => {
      doStep3(result2, (result3) => {
        console.log(`结果：${result3}`);
      });
    });
  });
}
doOperation();

```

``` js
const fetchPromise = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

console.log(fetchPromise);

fetchPromise.then((response) => {
  console.log(`已收到响应：${response.status}`);
});

console.log("已发送请求……");

```

我们在这里：
- 调用 fetch() API，并将返回值赋给 fetchPromise 变量。
- 紧接着，输出 fetchPromise 变量，输出结果应该像这样：Promise { \<state\>: "pending" }。这告诉我们有一个 Promise 对象，它有一个 state属性，值是 "pending"。"pending" 状态意味着操作仍在进行中。
- 将一个处理函数传递给 Promise 的 then() 方法。当（如果）获取操作成功时，Promise 将调用我们的处理函数，传入一个包含服务器的响应的 Response 对象。
- 输出一条信息，说明我们已经发送了这个请求。
请注意，已发送请求…… 的消息在我们收到响应之前就被输出了。与同步函数不同，fetch() 在请求仍在进行时返回，这使我们的程序能够保持响应性。响应显示了 200（OK）的状态码，意味着我们的请求成功了。

在你通过 fetch() API 得到一个 Response 对象的时候，你需要**调用另一个函数来获取响应数据**。在这里，我们想获得 JSON 格式的响应数据，所以我们会调用 Response 对象的 json() 方法。事实上，**json() 也是异步的**，因此我们必须连续调用两个异步函数。

``` js
const fetchPromise = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise.then((response) => {
  const jsonPromise = response.json();
  jsonPromise.then((json) => {
    console.log(json[0].name);
  });
});
```

Promise 的优雅之处在于 then() 本身也会返回一个 Promise，这个 Promise 将指示 then() 中调用的异步函数的完成状态。这意味着我们可以（当然也应该）把上面的代码改写成这样：

``` js
const fetchPromise = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
  .then((response) => response.json())
  .then((data) => {
    console.log(data[0].name);
  });
```

不必在第一个 then() 的处理程序中调用第二个 then()，我们可以直接返回 json() 返回的 Promise，并在该返回值上调用第二个 then()。这被称为 Promise 链，意味着当我们需要连续进行异步函数调用时，我们就可以避免不断嵌套带来的缩进增加。


**错误捕获**

为了支持错误处理，Promise 对象提供了一个 **catch()** 方法。这很像 then()：你调用它并传入一个处理函数。然后，当异步操作成功时，传递给 then() 的处理函数被调用，而当异步操作失败时，传递给 catch() 的处理函数被调用。

如果将 catch() 添加到 Promise 链的**末尾**，它就可以在任何异步函数失败时被调用。于是，我们就可以将一个操作实现为几个连续的异步函数调用，并在一个地方处理所有错误。


我们使用 catch() 添加了一个错误处理函数，并修改了 URL（这样请求就会失败）。


``` js
const fetchPromise = fetch(
  "bad-scheme://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);

fetchPromise
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP 请求错误：${response.status}`);
    }
    return response.json();
  })
  .then((json) => {
    console.log(json[0].name);
  })
  .catch((error) => {
    console.error(`无法获取产品列表：${error}`);
  });
```

**Promise术语**

Promise 有三种状态：
- **待定**（pending）：初始状态，既没有被兑现，也没有被拒绝。这是调用 fetch() 返回 Promise 时的状态，此时**请求还在进行中**。
- **已兑现**（fulfilled）：意味着操作成功完成。当 Promise 完成时，它的 **then() 处理函数被调用**。
- **已拒绝**（rejected）：意味着操作失败。当一个 Promise 失败时，它的 **catch() 处理函数被调用**。


有时你需要所有的 Promise 都得到实现，但它们并不相互依赖。在这种情况下，将它们一起启动然后在它们全部被兑现后得到通知会更有效率。这里需要 Promise.all() 方法。它接收一个 Promise 数组，并返回一个单一的 Promise。

由**Promise.all()**返回的 Promise：
- 当且仅当数组中所有的 Promise 都被兑现时，才会通知 then() 处理函数并提供一个包含所有响应的数组，数组中响应的顺序与被传入 all() 的 Promise 的顺序相同。
- 会被拒绝——如果数组中有任何一个 Promise 被拒绝。此时，catch() 处理函数被调用，并提供被拒绝的 Promise 所抛出的错误。

``` js
const fetchPromise1 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);
const fetchPromise2 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
);
const fetchPromise3 = fetch(
  "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
);

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((responses) => {
    for (const response of responses) {
      console.log(`${response.url}：${response.status}`);
    }
  })
  .catch((error) => {
    console.error(`获取失败：${error}`);
  });
```

这里我们向三个不同的 URL 发出三个 fetch() 请求。如果它们都被兑现了，我们将输出每个请求的响应状态。如果其中任何一个被拒绝了，我们将输出失败的情况。


``` js
const fetchPromise1 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);
const fetchPromise2 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
);
const fetchPromise3 = fetch(
  "bad-scheme://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
);

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((responses) => {
    for (const response of responses) {
      console.log(`${response.url}：${response.status}`);
    }
  })
  .catch((error) => {
    console.error(`获取失败：${error}`);
  });

```

这里三个请求中有一个失败都会触发catch函数

有时，你可能需要一组 Promise 中的某一个 Promise 的兑现，而不关心是哪一个。在这种情况下，你需要 **Promise.any()**。这就像 Promise.all()，不过在 Promise 数组中的任何一个被兑现时它就会被兑现，如果所有的 Promise 都被拒绝，它也会被拒绝。

与all相反，有一个兑现了都会返回200.

``` js
const fetchPromise1 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
);
const fetchPromise2 = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found",
);
const fetchPromise3 = fetch(
  "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json",
);

Promise.any([fetchPromise1, fetchPromise2, fetchPromise3])
  .then((response) => {
    console.log(`${response.url}：${response.status}`);
  })
  .catch((error) => {
    console.error(`获取失败：${error}`);
  });
```

**async和await**

async 关键字为你提供了一种更简单的方法来处理基于异步 Promise 的代码。在一个函数的开头添加 async，就可以使其成为一个异步函数。

在异步函数中，你可以在调用一个返回 Promise 的函数之前使用 **await** 关键字。这使得代码在该点上等待，直到 Promise 被完成，这时 Promise 的响应被当作返回值，或者被拒绝的响应被作为错误抛出。


``` js
async function fetchProducts() {
  try {
    // 在这一行之后，我们的函数将等待 `fetch()` 调用完成
    // 调用 `fetch()` 将返回一个“响应”或抛出一个错误
    const response = await fetch(
      "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json",
    );
    if (!response.ok) {
      throw new Error(`HTTP 请求错误：${response.status}`);
    }
    // 在这一行之后，我们的函数将等待 `response.json()` 的调用完成
    // `response.json()` 调用将返回 JSON 对象或抛出一个错误
    const json = await response.json();
    console.log(json[0].name);
  } catch (error) {
    console.error(`无法获取产品列表：${error}`);
  }
}

fetchProducts();
```

- - 这里我们调用 await fetch()，我们的调用者得到的并不是 Promise，而是一个完整的 Response 对象，就好像 fetch() 是一个同步函数一样。
我们甚至可以使用 try...catch 块来处理错误，就像我们在写同步代码时一样。
- 但请注意，这个写法只在异步函数中起作用。**异步函数总是返回一个 Promise**。


### 实现基于Promise的API

**实现alarm()API**

它将以被唤醒人的名字和一个在人被唤醒前以毫秒为单位的延迟作为参数。在延迟之后，本函数将会发送一个包含需要被唤醒人名字的 "Wake up!" 消息。

我们将会使用 **setTimeout()** 来实现 alarm() 函数。setTimeout() 以一个回调函数和一个以毫秒为单位的延迟作为参数。当调用 setTimeout() 时，它将启动一个设置为给定延迟的计时器，当时间过期时，它就会调用给定的回调函数。


### 框架的主要特性

**生命周期**

在框架上下文中，一个组件的生命周期是一个组件从被追加到 DOM 然后被浏览器渲染（通常称为挂载）到从 DOM 中移除（通常称为卸载）所经历的一系列阶段的集合。每个框架对这些生命周期阶段的命名都不同，而且不是所有的框架都能让开发者访问相同的阶段。所有的框架都遵循相同的一般模型：它们允许开发者在组件挂载、渲染和卸载以及这之间的许多阶段执行某些动作。s