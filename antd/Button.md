# button
## render
jsx结构如下：
```
return (
  <ComponentProp
    {...omit(others, ['loading'])}
    type={others.href ? undefined : (htmlType || 'button')}
    className={classes}
    onClick={this.handleClick}
  >
    {iconNode}{kids}
  </ComponentProp>
)
```
### ComponentProp

```
const ComponentProp = others.href ? 'a' : 'button';
```
组件根节点类型。

如果传入href,代表你期望button是一个超链接，组件将会渲染成一个a标签。

否则是button标签

### {...omit(others, ['loading'])}
将other里面除了loading属性以外的其他属性和方法直接应用于ComponentProp包裹组件。

### type
button的类型。

如果是a标签，则不需要该属性。否则type由htmlType属性决定，默认为button

### className
这里的classname根据传入的参数，利用classname库，做了一个合并。

```
const classes = classNames(prefixCls, className, {
  [`${prefixCls}-${type}`]: type,
  [`${prefixCls}-${shape}`]: shape,
  [`${prefixCls}-${sizeCls}`]: sizeCls,
  [`${prefixCls}-icon-only`]: !children && icon,
  [`${prefixCls}-loading`]: loading,
  [`${prefixCls}-clicked`]: clicked,
  [`${prefixCls}-background-ghost`]: ghost,
  [`${prefixCls}-two-chinese-chars`]: hasTwoCNChar,
});
```
### onClick
方法里面有一个延时的操作，用于添加操作的效果。

```
// Add click effect
this.setState({ clicked: true });
clearTimeout(this.timeout);
this.timeout = window.setTimeout(() => this.setState({ clicked: false }), 500);
```

```
[`${prefixCls}-clicked`]: clicked,
```
### iconNode

```
const iconNode = iconType ? <Icon type={iconType} /> : null;
```
icon图标

### kids

```
const kids = (children || children === 0)
  ? React.Children.map(children, child => insertSpace(child, this.isNeedInserted())) : null;
```
这里使用了React.Children.map这个可靠的方法。


## 语法

```
const kids = (children || children === 0)
  ? React.Children.map(children, child => insertSpace(child, this.isNeedInserted())) : null;
```


## 库

### classnames
合并classname

### omit.js
返回一个对象的浅拷贝，这个对象已经删除了一些属性