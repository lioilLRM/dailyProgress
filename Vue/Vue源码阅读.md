![[Pasted image 20241115174944.png]]

### 1. 如何解析标签里面指定的属性和值呢？
比如：sd-text、sd-show、sd-class
  
selector: "[sd-text],[sd-show],[sd-class],[sd-on]" 
`root.querySelectorAll(selector)`可以批量获取指定选择器的标签。

```js
 var self = this,
        root = this.el = document.getElementById(opts.id),
        els  = root.querySelectorAll(selector),
     ;[].forEach.call(els, processNode)


    // 处理节点，节点里面的属性值太多了。
    // 为了减少数据量，只需要关键属性值就可以了，可以筛选出需要的属性值。
    function processNode (el) {
        cloneAttributes(el.attributes).forEach(function (attr) {
            var directive = parseDirective(attr)
            if (directive) {
                bindDirective(self, el, bindings, directive)
            }
        })
    }
}

// clone attributes so they don't change
//  // 为了减少数据量，只需要关键属性值就可以了，可以筛选出需要的属性值。
function cloneAttributes (attributes) {
    return [].map.call(attributes, function (attr) {
        return {
            name: attr.name,
            value: attr.value
        }
    })
}
```


2. 销毁实例的方法：
```js
/**
 * 销毁实例：
 * 1. 解绑所有指令
 * 2. 从DOM中移除实例元素
 */
Seed.prototype.destroy = function () {
    for (var key in this._bindings) {
        this._bindings[key].directives.forEach(function (directive) {
            if (directive.definition.unbind) {
                directive.definition.unbind(
                    directive.el,
                    directive.argument,
                    directive
                )
            }
        })
    }
    this.el.parentNode.remove(this.el)
}
```


3. 问题：直接看源码的话，会容易陷入到细节里面，如何更好的看源码呢？
	1. 这个代码为了解决什么需求？因为什么需求，所以需要这个实现方式？





### 2. bind()方法的作用
在看源码的时候，老是看到有类似的bind()方法的存在，但是一直没有搞懂他们的意思；
比如：
```js
if (!Function.prototype.bind) {
    // Function.prototype.bind is a standard part of ECMAScript 5th Edition (December 2009, http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-262.pdf)
    // In case the browser doesn't implement it natively, provide a JavaScript implementation. This implementation is based on the one in prototype.js
    Function.prototype.bind = function (object) {
        var originalFunction = this, 
        args = Array.prototype.slice.call(arguments), 
        object = args.shift();
        
        return function () {
            return 
            originalFunction.apply(object, args.concat(Array.prototype.slice.call(arguments)));
        }; 
    };
}
```

上面的代码中，存在了几个盲区：
1. `arguments`: 是一个类数组对象
2. args = Array.prototype.slice.call(arguments)
   1. 这函数的作用是将一个[[类数组]]转为数组的JS技巧。
   2. slice函数的返回值是从一个数组中返回一个新的数组。
   3. 
3. object = args.shift()， 中的shift()


