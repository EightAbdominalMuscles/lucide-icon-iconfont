# lucide-icon-iconfont
lucide-icon在 iconfont的库, 放在iconfont上是为了让小程序也支持lucide-icon https://www.iconfont.cn/collections/detail?cid=53746

### 步骤1 lucide-icon去别名, 找到网页里真正调用的SVG的名字
如 lucide-react 这些包里面的icon有可能使用的时候叫 “AlertCircle” 但是真正的SVG名字是 “circle-alert”  iconfont里存储的是 SVG的名字并不是别名,可以用AI找出来lucide-react 图标对应的原始 SVG 文件名（真正的图标名称）
+ 可以对AI说“找到项目中所有使用过的 lucide-react 图标对应的原始 SVG 文件名（真正的图标名称）”
### 步骤二 在iconfont新建项目, 将使用的iconfont添加到项目中
1. 在https://www.iconfont.cn/中采用font class的方式下载下来
2. 创建小程序组件 components/components/icon组件
```js
/**
 * Icon Component (iconfont)
 * Usage: <l-icon name="home" size="48" color="#059669" />
 */
Component({
    properties: {
        name: {
            type: String,
            value: ''
        },
        size: {
            type: Number,
            value: 48
        },
        color: {
            type: String,
            value: ''
        }
    }
})
```
components/icon/icon.json
```json
{
  "component": true,
  "styleIsolation": "apply-shared"
}
```
components/icon/icon.wxml
```wxml
<text wx:if="{{name}}" class="iconfont icon-{{name}}"
    style="font-size: {{size}}rpx;{{color ? ' color: ' + color + ';' : ''}}" />
components/icon/icon.wxss
```
/* Icon Component Styles */
```style
.iconfont {
    display: inline-block;
    vertical-align: middle;
    line-height: 1;
}
```
11、配置为小程序全局组件

app.json
```json
{
    "usingComponents": {
        "l-icon": "/components/icon/icon"
    },
    ......
}
```
12、业务页面引用
```html
<l-icon name="log-in" size="44" />
```


