<script setup lang="ts">
import { HotTable } from "@handsontable/vue3";
import { TextEditor } from "handsontable/editors/textEditor";
import { registerAllModules } from "handsontable/registry";
import "handsontable/dist/handsontable.full.min.css";

// register Handsontable's modules
registerAllModules();

class CustomEditor extends TextEditor {
  createElements() {
    super.createElements();

    this.TEXTAREA = document.createElement("input");
    this.TEXTAREA.setAttribute("placeholder", "Custom placeholder");
    this.TEXTAREA.setAttribute("data-hot-input", 'true');
    this.textareaStyle = this.TEXTAREA.style;
    this.TEXTAREA_PARENT.innerText = "";
    this.TEXTAREA_PARENT.appendChild(this.TEXTAREA);
  }
}

const hotSettings = {
  startRows: 5,
  columns: [
    {
      editor: CustomEditor,
    },
  ],
  colHeaders: true,
  colWidths: 200,
  licenseKey: "non-commercial-and-evaluation",
};
</script>

<template>
  <div id="example1">
    <hot-table :settings="hotSettings"></hot-table>
  </div>
</template>
