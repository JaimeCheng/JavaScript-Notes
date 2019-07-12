# 2. 在 HTML 中使用 JavaScript

## `<script>`的6个属性   <a id="script"></a>

* `async` 表示应该立即下载脚本，但不应妨碍页面中的其他操作，比如下载其他资源或 等待加载其他脚本。当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。只对外部脚本文件有效；
* `defer` 表示脚本可以延迟到文档完全被解析和显示之后再执行。延迟脚本总是按照指定它们的顺序执行。只对外部脚本文件有效；
* `src` 外部文件；
* `type` 最大限度兼容性的值 `text/javascript`；
* `charset` 大多浏览器会忽略；
* `language` 已废弃；

## JS代码的加载顺序，结合上述属性   <a id="load-order"></a>

## 声明文档类型，文档模式的影响   <a id="document-modes"></a>

* **混杂模式**，是不可取的，因为其没有兼容性可言。在IE（IE6~IE9）中，混杂模式即使用IE5.5内核来解析并渲染页面；
* **标准模式**，让 IE 的行为更接近标准行为；
* **准标准模式**，这种模式下的浏览器特性有很多都是符合标准的，但也不尽然。不标准的 地方主要体现在处理图片间隙的时候\(在表格中使用图片时问题最明显\)；

```markup
<!-- 对于标准模式，可以通过使用下面任何一种文档类型来开启： -->
<!-- HTML 4.01 严格型 -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<!-- XHTML 1.0 严格型 -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<!-- HTML 5 -->
<!DOCTYPE html>
```

## 考虑禁用JavaScript的场景   <a id="no-script"></a>

```markup
<!-- 浏览器不支持脚本; 浏览器支持脚本，但脚本被禁用，会显示以下 -->
<noscript> 
  <p>本页面需要浏览器支持(启用)JavaScript。</p>
</noscript>
```

