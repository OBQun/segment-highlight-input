# 静态模板

这是一个用于 HTML 文档的静态模板。它不涉及任何捆绑器或捆绑过程。您可以将其作为项目的起点！

## 使用方法

1. 克隆该仓库或下载 `index.html` 文件。
2. 在您偏好的网络浏览器中打开 `index.html` 文件。
3. 通过点击可编辑的段落并键入您自己的文本来编辑内容。
4. 文本将自动分段为句子。
5. 当您选择不同的段落时，它们将以红色进行高亮显示。

## 示例

以下是静态模板的示例：

---

这是一个静态模板。没有任何捆绑器或捆绑过程！欢迎使用！

---

## 自定义

您可以根据需要自定义模板。您可以根据需要修改 HTML、CSS 和 JavaScript 代码。

### HTML

模板的 HTML 结构如下所示：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Head content -->
  </head>
  <body>
    <p contenteditable id="text"></p>
    <script>
      // JavaScript code
    </script>
  </body>
</html>
```

您可以添加其他 HTML 元素或修改现有元素。

### CSS

`<style>` 部分中的 CSS 代码可用于样式化元素。目前，它仅包含了一个用于 `#text` 元素的规则：

```css
<style>
  #text {
    outline: none;
  }
  #text::highlight(selected) {
    color: red;
  }
</style>
```

您可以根据自己的喜好更新样式。

### JavaScript

`<script>` 部分中的 JavaScript 代码处理了选择更改事件，并执行了分段和高亮显示的操作：

```javascript
<script>
  const textEl = document.querySelector("#text");
  textEl.innerText = `这是一个静态模板。没有任何捆绑器或捆绑过程！欢迎使用！`;

  const segmenter = new Intl.Segmenter("en", { granularity: "sentence" });

  document.addEventListener("selectionchange", (e) => {
    const target = document.activeElement;
    const segments = [...segmenter.segment(target.innerText)];
    const index = segments.findIndex(
      ({ index }) => index > window.getSelection().anchorOffset
    );

    const segment = segments[(index === -1 ? segments.length : index) - 1];

    console.log(segment);

    const range = document.createRange();
    range.setStart(target.firstChild, segment.index);
    range.setEnd(
      target.firstChild,
      segment.index + segment.segment.length
    );
    const highlight = new Highlight(range);
    CSS.highlights.set("selected", highlight);
  });
</script>
```

您可以修改 JavaScript 代码以添加其他功能或更改分段行为。

## 许可证

该模板以 [MIT 许可证](LICENSE) 发布。请随意使用和修改它用于您自己的项目。

祝您使用愉快！
