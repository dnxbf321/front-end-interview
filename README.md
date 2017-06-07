# 前端笔试题

_注意：答题前请fork这个仓库，然后把笔试答案（包括相关代码）整理好，放到fork的仓库里；需要在线演示的代码，可以放到jsfiddle、codepen或者类似的服务上面。_

__1. 以下代码有没有什么问题？ 如果有，如何改进。__

关系: Post belongs_to Author

```ruby
posts = Post.limit(50)
posts.each do |post|
  puts post.author.name
end
```

posts 的 author 相同，posts.each 打印出来的 author.name 是一样的，没必要做循环

代码修改为

```ruby
posts = Post.limit(50)
puts posts.first.author.name
```


__2. 我们通常只希望在 controllers 只出现 7 个标准的 action，以下 controller 如何改进？__

```ruby
class PostsController < ApplicationController
    def show
    end

    def index
    end

    def create
    end

    def archive
    end

    def vote
    end

    def share
    end
end
```

7 个标准的 action 分别是 index, show, new, edit, update, destroy, create，本题中的 archive/vote/share 不在范围之类。使用 update 代替，archive/vote/share 三种不同的操作可使用参数进行区分

修改：

```ruby
class PostsController < ApplicationController
    def show
    end

    def index
    end

    def create
    end

    def update
        // 假设参数的键是 act
        actType = params[:act]

        // then do diffreent things
    end
end
```


__3. 下图中，.container和.box的高度和宽度都是浮动的、不确定的，编写一段CSS，让.box元素在水平方向和竖直方向相对于.container容器居中，要求至少采用三种不同的实现方式，并分析它们的使用场景和优缺点__

要求：不能引入除了.box和.container以外的元素辅助布局

![question 3](https://raw.githubusercontent.com/mycolorway/front-end-interview/master/images/q4.png)

[https://jsfiddle.net/Lrns47yg/1/](https://jsfiddle.net/Lrns47yg/1/)

__4. 继续上一题，请使用CoffeeScript和Sass编写代码，实现切换.box元素的显示（display:block）和隐藏（display：none）状态的交互__

要求：
* 实现这样的交互动画：显示的时候从下往上移动一段距离到居中，同时opacity从0到1变化；隐藏的时候从居中位置往下移动一段距离，同时opacity从1变化到0
* 隐藏状态下，.box的`display`需要设置为`none`
* 使用css trasition实现动画交互，不能使用setTimeout方法
* 进行合理的模块化设计，让代码易读、易维护、易扩展

[https://jsfiddle.net/5jLvsbaa/4/](https://jsfiddle.net/5jLvsbaa/4/)

__5. 观察下面的截图，只从视觉设计上考虑，有哪些地方做的不好，应该怎样改进？__

![question 5](https://raw.githubusercontent.com/mycolorway/front-end-interview/master/images/q6.png)

答

- 分块不合理。开通管理员和二维码这部分我先称它为上层，logo 蓝色和下部灰色区域我先称它为下层。下层没有必要再划分成蓝灰两块，因为没有内容需要区分。

- 内容主次安排不合理。页面主要内容是扫码，二维码并没有置于页面中央，而是处于页面内容最下方。扫码的辅助文案可以放在二维码下方，二维码可以往上挪一些。logo 对比度高、显眼，可以缩小一些并移到左上角，避免视觉上的干扰。
