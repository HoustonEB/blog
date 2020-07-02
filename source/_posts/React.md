---
title: React
date: 2020-6-30 11:46:11
categories: React
tags:
 - React
---
### React Refs转发
1. 在函数式组件中转发

```js
const Button = React.forwardRef(function (props, ref) {
    return h.button('', {
        ref,
        onClick: props.onClick
    }, 
    props.children
    );
})
export default class View extends Component {
    btnRef;
    constructor(props) {
        super(props);
        this.btnRef = React.createRef();
    }

    render() {

        return (
            h.div('', {},
                h(Button, {ref: this.btnRef}, 'dom转发'),
                h(Button, {}, '未dom转发'),
                h(Button, {
                    onClick: () => {console.log(this.btnRef, '子组件btnDom')}
                }, '获取子组件dom')
            )
        )
    }
}
// btnRef输出: {current: button}
```
<!-- more -->
2. 在高阶组件中转发

```js
const Button = React.forwardRef(function (props, ref) {
    return h.button('', {
        ref,
        ...props
    },
        props.children
    );
})
const wrapComp = function (component) {
    class wrapCompView extends React.Component {
        constructor(props) {
            super(props);
        };

        render() {
            let { forwardedRef, children, ...rest } = this.props;
            return h(component, {
                ref: forwardedRef,
                ...rest
            }, children);
        }
    }
    return React.forwardRef((props, ref) => {
        return h(wrapCompView, { forwardedRef: ref, ...props }, props.children);
    })
}
export default class View extends Component {
    btnRef;
    wrapBtnComp;

    constructor(props) {
        super(props);
        this.btnRef = React.createRef();
        this.wrapBtnComp = wrapComp(Button);
    }

    render() {

        return (
            h.div('', {},
                h(this.wrapBtnComp, { ref: this.btnRef }, 'dom转发'),
                h(Button, {
                    onClick: () => { console.log(this.btnRef, '子组件btnDom') }
                }, '获取子组件dom')
            )
        )
    }
}
```
{% note danger %}
1.第二个参数 ref 只在使用 React.forwardRef 定义组件时存在。常规函数和 class 组件不接收 ref 参数，且 props 中也不存在 ref。
2.Ref 转发不仅限于 DOM 组件，你也可以转发 refs 到 class 组件实例中。
3.上面的示例有一点需要注意：refs 将不会透传下去。这是因为 ref 不是 prop 属性。就像 key 一样，其被 React 进行了特殊处理。如果你对 HOC 添加 ref，该 ref 将引用最外层的容器组件，而不是被包裹的组件
{% endnote %}
---
### Hook
