```scss
$namespace: 'tb';
$element-separator: '__';
$modifier-separator: '--';
$state-prefix: 'is-';


@mixin tb-b($block) {
  $B: $namespace+'-'+$block !global; // 定义一个全局变量 $B，表示完整的块名
  .#{$B} {
    @content;
  }
}

```
通过 `#{}` 插值语句可以在选择器或属性名中使用变量：
```
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```

编译为

```
p.foo {
  border-color: blue; 
  }
```
 使用动态选择器 `.#{$B}` 创建一个块选择器，实际上是 `.tb-button`。
 
 变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 `!global` 声明：

```
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
```

编译为

```
#main {
  width: 5em;
}

#sidebar {
  width: 5em;
}
```