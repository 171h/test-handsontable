<script setup lang="ts">
import { HotTable } from "@handsontable/vue3";
import { registerAllModules } from "handsontable/registry";
import { GridSettings } from "handsontable/settings";
import "handsontable/dist/handsontable.full.min.css";

// register Handsontable's modules
registerAllModules();

function safeHtmlRenderer(instance, td, row, col, prop, value, cellProperties) {
  // WARNING: Be sure you only allow certain HTML tags to avoid XSS threats.
  // Sanitize the "value" before passing it to the innerHTML property.
  td.innerHTML = value;
}

function coverRenderer(instance, td, row, col, prop, value, cellProperties) {
  const img = document.createElement('img');

  img.src = value;

  img.addEventListener('mousedown', event => {
    event.preventDefault();
  });

  td.innerText = '';
  td.appendChild(img);

  return td;
}

const hotSettings: GridSettings = reactive({
  data: [
    {
      title:
        '<a href="https://www.amazon.com/Professional-JavaScript-Developers-Nicholas-Zakas/dp/1118026691">Professional JavaScript for Web Developers</a>',
      description:
        'This <a href="https://bit.ly/sM1bDf">book</a> provides a developer-level introduction along with more advanced and useful features of <b>JavaScript</b>.',
      comments: "I would rate it &#x2605;&#x2605;&#x2605;&#x2605;&#x2606;",
      cover: "https://handsontable.com/docs/img/examples/professional-javascript-developers-nicholas-zakas.jpg",
    },
    {
      title: '<a href="https://shop.oreilly.com/product/9780596517748.do">JavaScript: The Good Parts</a>',
      description:
        "This book provides a developer-level introduction along with <b>more advanced</b> and useful features of JavaScript.",
      comments: "This is the book about JavaScript",
      cover: "https://handsontable.com/docs/img/examples/javascript-the-good-parts.jpg",
    },
    {
      title: '<a href="https://shop.oreilly.com/product/9780596805531.do">JavaScript: The Definitive Guide</a>',
      description:
        "<em>JavaScript: The Definitive Guide</em> provides a thorough description of the core <b>JavaScript</b> language and both the legacy and standard DOMs implemented in web browsers.",
      comments:
        'I\'ve never actually read it, but the <a href="https://shop.oreilly.com/product/9780596805531.do">comments</a> are highly <strong>positive</strong>.',
      cover: "https://handsontable.com/docs/img/examples/javascript-the-definitive-guide.jpg",
    },
  ],
  columns: [
    {
      title: "Title",
      data: "title",
      renderer: 'html',
      width: 200,
    },
    {
      title: 'Description',
      data: 'description',
      renderer: 'html',
      width: 200,
    },
    {
      title: 'Comments',
      data: 'comments',
      renderer: safeHtmlRenderer,
      width: 200,
    },
    {
      title: 'Cover',
      data: 'cover',
      renderer: coverRenderer,
      width: 80,
    }
  ],
  colHeaders: true,
  rowHeights: 55,
  height: "auto",
  licenseKey: "non-commercial-and-evaluation",
})



</script>

<template>
  <div id="example1">
    <hot-table :settings="hotSettings"></hot-table>
  </div>
</template>
