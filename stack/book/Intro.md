## 简介

### 初识流程图


[![](../images/intro/all-page-stack-reconciler-25-scale.jpg)](../images/intro/all-page-stack-reconciler.svg)

<em>Intro.0 整体流程 (clickable)</em>

花点时间看看这幅流程图。整体看起来有点复杂，但实际上只包括两个流程：挂载和更新。我（作者）跳过了卸载部分，因为那有点像挂载的逆过程，移除它会让流程图变简单。当然，这幅图不是
100% 与源码对应的，但囊括了主要的部分。总的来说，这大概有 60%，剩下的 40%
只能带来微小的视觉价值。所以为了简单，我省略了它们。

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

如你所见，有些项会有两个。这表示它们对每个平台有不同的实现。举个简单的例子，像
ReactEventListener，它的实现会根据平台的不同而不同。从技术上讲，你可以想象这些依赖于某一平台的模块将以某些方式注入或者连接到当前的逻辑流程。事实上，的确有很多注入器，因为它们的使用是标准的组合模式的一部分，我选择忽略它们。再一次，为了简单。

让我们中常规浏览器中学习 React DOM 逻辑流程。它是最常用的，完全涵盖所有的 React 架构思想。所以，这足够了。


### 代码示例

学习框架或者库源码的最佳方式是什么？没错，就是阅读和调试代码。好的，我们准备调试两个流程：**ReactDOM.render** 和
**component.setState**，它们分别对应挂载和更新。让我们来检查一下我们的代码，我们需要什么？可能是几个具有简单渲染功能的小组件，调试更加容易。 

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

准备完毕，我们可以开始了。让我们继续谈谈流程中的第一部分。我们将一步一步的完成整个流程。

[To the next page: Part 0 >>](./Part-0.md)


[Home](../../README.md)
