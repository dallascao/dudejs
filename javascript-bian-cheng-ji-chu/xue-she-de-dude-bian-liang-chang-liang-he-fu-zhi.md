# 学舌的 Dude - 变量、常量和赋值



{% hint style="info" %}
[点击这里](https://dudejs.gt4t.ai/1.get_started/dude-Hello_world!.zip)下载项目zip包。复制到容易找到的地方，例如桌面。解压后出现 `dude-Hello_world!` 文件夹。用 `vscode` 打开文件夹，再打开 `game.js`。
{% endhint %}

​

### 变量

第102行，我们也将 `Hello`  修改为 `Hello world`  的地方改成下面这个样子：

{% code overflow="wrap" %}
```javascript
    let userMessage = "hello, beautiful world!";
    this.speechBubble = this.add.text(this.player.x, this.player.y - 50, userMessage, {
        font: "16px Arial",
        fill: "#000", 
        backgroundColor: "#fff",
        padding: { x: 5, y: 5 }
    }).setVisible(false);
```
{% endcode %}

即我们在原来102行上面，增加了一行

```javascript
    let userMessage = "hello, beautiful world!";
```

然后把102行原来写 `"Hello World"`的地方换成了 `userMessage`。注意这里的 `userMessage`不能加引号。点 `Visual Studio`右下角的 `live server`运行。`Dude`现在会说 `hello, beautiful world!`

在这里，我们用 `let`定义了一个叫 `userMessage`的变量，可以把变量想象成一个盒子，在大多数编程语言里， `=`表示的是把值保存在变量里。如上面这一行，用翻译成汉语，即，定义一个叫 \`usermessage\` 的变量，并把 `hello, beautiful world!`放（`=`）到一个叫这个叫`userMessage`的变量盒子里。

```lua
                           "hello, beautiful world!"
                                      |
                                      v
                          +---------------------------+
                          |       userMessage         |
                          | "hello, beautiful world!" |
                          +---------------------------+
                       
```

### 变量赋值

1. 给一个变量赋了新值后，旧的值就被丢弃，被覆盖了，也就是说这个装内容的变量盒子只能装一个东西：

{% hint style="success" %}
<pre class="language-javascript" data-line-numbers><code class="lang-javascript"><strong>let userMessage = "Hello, beautiful world!";
</strong><strong>userMessage = "Hello. I am a start collector.";
</strong></code></pre>
{% endhint %}

我们的代码会一行一行地跑，等跑到第二行的时候，变量 \`userMessage\`的值改变了，自此之后，它的内容就是新的内容了。

2. 注意第二行我们给已经定义过的 `userMessage`变量赋新值时，不再需要先写 `let`。也就是说，变量在使用前应用 `let`定义，但只能定义一次。下面的代码会出错。

{% hint style="danger" %}
```javascript
let userMessage = "Hello, beautiful world!";
let userMessage = "Hello. I am a start collector.";
```
{% endhint %}



### 常量和常量赋值

有些值是不需要改变的，我们常常也需要给这些值起一个好记的名字。例如π的值是 3.141592654，我们不想每次使用它的时候都输入这么难记的数字，我们可以先把它保存在一个常量盒子里。等需要用这个数字时，用这个好记的常量的名字代替即可。我们可用下面的代码来计算出圆的面积：

{% code lineNumbers="true" %}
```javascript
const pi = 3.141592654;
let r = 7;
const area1 = pi * r * r;
r=11;
const area2 = pi * r * r;
```
{% endcode %}

运行了上面的代码之后常量 `area1`里保存了半径为 7 的圆的值，\`area2\`里保存了半径为 11 的圆的值。注意第 4 行和第 2 行的不同。我们在第 2 行定义了半径变量 `r` 并在里面放了 7，在第 4 行我们改变了 `r`的内容，在里面放了 11。从此之后 `r`的值就不再是 7，而是 11 了。 &#x20;

### 实战一

现在我们回到我们 `Dude`，我们把开头的 101 行  `let userMessage = "hello, beautiful world!";`   改为 `let userMessage = prompt("");`

```javascript
let userMessage = prompt(""); 
this.speechBubble = this.add.text(this.player.x, this.player.y - 50, userMessage, {
    font: "16px Arial",
    fill: "#000", 
    backgroundColor: "#fff",
    padding: { x: 5, y: 5 }
}).setVisible(false);
```

&#x20;`let userMessage = prompt("");`的意思是定义变量 `userMessage`，把用户输入内容保存在 `userMessage`里。运行时用户会收到一个输入框，用户输入内容后，`Dude`变成了鹦鹉，反复说用户输入的内容了。

### 实战二

按左箭头，`Dude`向左走，按右箭头向右走。这是由 114 行以下代码实现的。

```javascript
    if (this.cursors.left.isDown) {        
        this.player.setVelocityX(-160);
        this.player.anims.play('left', true);
    } else if (this.cursors.right.isDown) {
        this.player.setVelocityX(160);
        this.player.anims.play('right', true);
    } else {
        this.player.setVelocityX(0);
        this.player.anims.play('turn');
    }
```

即用户按下左键时，`Dude`向左以 160 的速度移动，负值代表向左；同样，按下右键时，向右以同样的速度移动。

假设突然起了风，`Dude`向右走的时候顺风变快，向右走的时候顺风变快。我们该怎么写代码实现呢？

1. 假定风速不变，是个常量，我们可以在上面加上一行 `const windSpeed = 30 ;`，即定义一个叫 `windSpeed`的常量，并把值 30 赋给它。
2. 我们还可定义两个变量`dudeLeftVelocity`和 `dudeRightVelocity`，分别代表 `Dude`向左走时的速度和向右走时的速度。

更新后的代码：

```javascript
    const windSpeed = 30;
    let dudeLeftVelocity= -160 + windSpeed; let dudeRightVelocity = 160 + windSpeed;
    
    if (this.cursors.left.isDown) {        
        this.player.setVelocityX(dudeLeftVelocity);
        this.player.anims.play('left', true);
    } else if (this.cursors.right.isDown) {
        this.player.setVelocityX(dudeRightVelocity);
        this.player.anims.play('right', true);
    } else {
        this.player.setVelocityX(0);
        this.player.anims.play('turn');
    }
```

注意我们除了增加了两行代码之外，还把原来的 -160 改为了变量名称 `dudeLeftVelocity`，160 改为了 `dudeRightVelocity`。

好了，休息一下，点一下 `Visual Studio Code`右下角的`Live server`启动我们更新的游戏！



{% embed url="https://dudejs.gt4t.ai/2.variables_constants/dude-parrot/" %}

[点击这里](https://dudejs.gt4t.ai/2.variables_constants/dude-parrot.zip)下载更新后的`Dude`源代码。大胆些，随意更改这些代码来练习以上内容，例如你可改下 `Dude`跳起的高度。改坏了当然也很正常，大不了重新下载再来！

### 进阶思考

1. 我们设计出变量和常量是要解决什么问题？1) 实际的值可能会很长，很难记，把它保存在变量或常量里，使用变量或常量名代替实际的值，复用时更方便；2) 使用变量或常量实现数值的传递，即把一个常量或变量的值经过计算后再保存在另一个常量或变量中。
2. 你是不是觉得变量比常量更常用？都用变量不是照样跑？常量似乎没什么用？恰恰相反:-) 最佳实践是尽量多用常量而少用变量。[`Douglas Crockford`](https://en.wikipedia.org/wiki/Douglas_Crockford)甚至建议不用变量。原因是如果代码比较长，变量值常常发生变化，可能变得难以跟踪，在写后面的代码时很难确定它现在是什么样的值，从而造成问题和麻烦。不过这个问题一时不理解也没关系，写多了就知道了。现在写代码时先习惯多使用 `const`而不是`let`就行了。
