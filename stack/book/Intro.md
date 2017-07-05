## 简介

### 初识流程图


[![](../images/intro/all-page-stack-reconciler-25-scale.jpg)](../images/intro/all-page-stack-reconciler.svg)

<em>Intro.0 整体流程 (clickable)</em>

花点时间看看这幅流程图。整体看起来有点复杂，但实际上只包括两个流程：挂载和更新。我（作者）跳过了卸载部分，因为那有点像挂载的逆过程，移除它会让流程图变简洁。当然，这幅图不是
100% 与源码对应的，但囊括了主要的部分。总的来说，这大概有 60%，剩下的 40%
只能带来微小的视觉价值。所以为了简洁，我省略了它们。

第一眼你可能会发现这幅图有许多种颜色，每个逻辑项（图中的图形）将会与它的父模块有相同颜色的高亮。举个例子，当 ‘methodA’ 被红色的
‘methodB’ 调用时，‘methodA’ 也是红色的。下面是流程图中的图例以及每个文件的路径说明。

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-src-path.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-src-path.svg)

<em>Intro.1 模块颜色 (clickable)</em>

让我们将它们放到流程图中看看模块之间的依赖关系。

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/files-scheme.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/files-scheme.svg)

<em>Intro.2 模块依赖 (clickable)</em>

你或许知道，React 支持在多种环境中构建。
- Mobile (**ReactNative**)
- Browser (**ReactDOM**)
- Server Rendering
- **ReactART** (用于使用React绘制矢量图形)
- etc.

结果，一些文件实际比上面的流程图中描述的更大。以下是多环境通用的流程图。

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-per-platform-scheme.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-per-platform-scheme.svg)

<em>Intro.3 平台依赖 (clickable)</em>

As you can see, some items seem doubled. It shows they have a separate implementation for each platform. Let’s take something simple, like ReactEventListener. Obviously, its implementation will be different for different platforms! Technically, as you can imagine, these platform dependent modules should be somehow injected or connected to the current logic flow, and, in fact, there are many such injectors. Because their usage is part of a standard composition pattern, I chose to omit them. Again, for simplicity.

Let’s learn the logic flow for **React DOM in a regular browser**. It’s the most used one, and it completely covers all React’s architecture ideas. So, fair enough!


### Code sample

What is the best way to learn the code of a framework or library? That's right, read and debug the code. Alright, we are gonna to debug **two processes**: **ReactDOM.render** and **component.setState**, which map on mount and update. Let’s check the code we can write for a start. What do we need? Probably several small components with simple renders, so it will be easier to debug.

```javascript
class ChildCmp extends React.Component {
    render() {
        return <div> {this.props.childMessage} </div>
    }
}

class ExampleApplication extends React.Component {
    constructor(props) {
        super(props);
        this.state = {message: 'no message'};
    }

    componentWillMount() {
        //...
    }

    componentDidMount() {
        /* setTimeout(()=> {
            this.setState({ message: 'timeout state message' });
        }, 1000); */
    }

    shouldComponentUpdate(nextProps, nextState, nextContext) {
        return true;
    }

    componentDidUpdate(prevProps, prevState, prevContext) {
        //...
    }

    componentWillReceiveProps(nextProps) {
        //...
    }

    componentWillUnmount() {
        //...
    }

    onClickHandler() {
        /* this.setState({ message: 'click state message' }); */
    }

    render() {
        return <div>
            <button onClick={this.onClickHandler.bind(this)}> set state button </button>
            <ChildCmp childMessage={this.state.message} />
            And some text as well!
        </div>
    }
}

ReactDOM.render(
    <ExampleApplication hello={‘world’} />,
    document.getElementById('container'),
    function() {}
);
```

So, we are ready to start, let’s move on to the first part of the scheme. One by one part we will go through all of it.

[To the next page: Part 0 >>](./Part-0.md)


[Home](../../README.md)
