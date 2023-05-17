<script setup lang="ts">
import { HotTable } from "@handsontable/vue3";
import { textRenderer } from "handsontable/renderers";
import { BaseEditor } from "handsontable/editors";
import { TextEditor } from "handsontable/editors/textEditor";
import { SelectEditor } from "handsontable/editors";
import { registerAllModules } from "handsontable/registry";
import { registerCellType } from "handsontable/cellTypes";
import { GridSettings } from 'handsontable/settings'
import "handsontable/dist/handsontable.full.min.css";
import { Logger } from '@171h/log'

// register Handsontable's modules
registerAllModules();

registerCellType('custom', {
  renderer: textRenderer,
  className: 'my-cell',
  readOnly: true,
  myCustomProperty: 'foo-custom',
})

const logger = new Logger('Editor')

class PassWordEditor extends TextEditor {
  createElements() {
    super.createElements();

    this.TEXTAREA = this.hot.rootDocument.createElement("input");
    this.TEXTAREA.setAttribute("type", "password");
    this.TEXTAREA.setAttribute("data-hot-input", "true");
    this.textareaStyle = this.TEXTAREA.style;
    this.textareaStyle.border = "none";
    this.textareaStyle.boxShadow = "none";
    this.textareaStyle.width = "0";
    this.textareaStyle.height = "0";
    this.TEXTAREA_PARENT.innerText = "";
    this.TEXTAREA_PARENT.appendChild(this.TEXTAREA);
  }
}

// class SelectEditor extends BaseEditor {
//   /**
//    * Initializes editor instance, DOM Element and mount hooks.
//    */
//    init() {
//     logger.info('init', 'start...')
//     // Create detached node, add CSS class and make sure its not visible
//     this.select = this.hot.rootDocument.createElement('SELECT');
//     this.select.classList.add('htSelectEditor');
//     this.select.style.display = 'none';

//     // Attach node to DOM, by appending it to the container holding the table
//     this.hot.rootElement.appendChild(this.select);
//     logger.debug('init', 'this', this)
//   }

//   // Create options in prepare() method
//   prepare(row, col, prop, td, originalValue, cellProperties) {
//     logger.info('prepare', 'start...')
//     // Remember to invoke parent's method
//     super.prepare(row, col, prop, td, originalValue, cellProperties);

//     const selectOptions = this.cellProperties.selectOptions;
//     let options;

//     if (typeof selectOptions === 'function') {
//       options = this.prepareOptions(selectOptions(this.row, this.col, this.prop));
//     } else {
//       options = this.prepareOptions(selectOptions);
//     }

//     this.select.innerText = '';

//     Object.keys(options).forEach((key) => {
//       const optionElement = this.hot.rootDocument.createElement('OPTION');
//       optionElement.value = key;
//       optionElement.innerText = options[key];
//       this.select.appendChild(optionElement);
//     });
//   }

//   prepareOptions(optionsToPrepare) {
//     logger.info('prepareOptions', 'start...')
//     let preparedOptions = {};

//     if (Array.isArray(optionsToPrepare)) {
//       for (let i = 0, len = optionsToPrepare.length; i < len; i++) {
//         preparedOptions[optionsToPrepare[i]] = optionsToPrepare[i];
//       }

//     } else if (typeof optionsToPrepare === 'object') {
//       preparedOptions = optionsToPrepare;
//     }

//     return preparedOptions;
//   }

//   onBeforeKeyDown(event: KeyboardEvent) {
//     logger.info('onBeforeKeyDown', 'start...')
//     const previousOptionIndex = this.select.selectedIndex - 1;
//     const nextOptionIndex = this.select.selectedIndex + 1;
//     logger.debug('onBeforeKeyDown', 'event.keyCode 0', event.keyCode)

//     switch (event.keyCode) {
//       case 38: // Arrow Up
//         logger.debug('onBeforeKeyDown', 'event.keyCode 38', event.keyCode)
//         if (previousOptionIndex >= 0) {
//           this.select[previousOptionIndex].selected = true;
//         }

//         event.stopImmediatePropagation();
//         event.preventDefault();
//         break;

//       case 40: // Arrow Down
//         logger.debug('onBeforeKeyDown', 'event.keyCode 40', event.keyCode)
//         if (nextOptionIndex <= this.select.length - 1){
//           this.select[nextOptionIndex].selected=true;
//         }

//         event.stopImmediatePropagation();
//         event.preventDefault();
//         break;

//       default:
//         logger.debug('onBeforeKeyDown', 'event.keyCode default', event.keyCode)
//         break;
//     }
//   }
//   getValue() {
//     logger.info('getValue', 'start...')
//     return this.select.value;
//   }

//   setValue(value) {
//     logger.info('setValue', 'start...')
//     this.select.value = value;
//   }

//   open() {
//     logger.info('open', 'start...')
//     const {
//       top,
//       start,
//       width,
//       height,
//     } = this.getEditedCellRect();
//     const selectStyle = this.select.style;

//     this._opened = true;

//     selectStyle.height = `${height}px`;
//     selectStyle.minWidth = `${width}px`;
//     selectStyle.top = `${top}px`;
//     selectStyle[this.hot.isRtl() ? 'right' : 'left'] = `${start}px`;
//     selectStyle.margin = '0px';
//     selectStyle.display = '';
//     this.hot.addHook('beforeKeyDown', (event: KeyboardEvent) => this.onBeforeKeyDown(event));
//   }

//   focus() {
//     logger.info('focus', 'start...')
//     this.select.focus();
//   }

//   close() {
//     logger.info('close', 'start...')
//     this._opened = false;
//     this.select.style.display = 'none';
//     this.hot.removeHook('beforeKeyDown', () => {});
//   }
// }

const hotSettings: GridSettings = {
  data: [
    ["", "Kia", "Nissan", "Toyota", "Honda"],
    ["2008", 10, 11, 12, 1311],
    ["2009", 20, 11, 14, 1345],
    ["2010", 30, 15, 12, 1345],
  ],
  columns: [
    {
      type: 'date',
      dateFormat: 'YYYY/MM/DD',
      correctFormat: true,
      defaultDate: '01/01/1900',
      datePickerConfig: {
        firstDay: 1,
        showWeekNumber: true,
        numberOfMonths: 1,
        i18n: {
          previousMonth : 'Previous Month',
          nextMonth     : 'Next Month',
          months        : ['1月','February','March','April','May','June','July','August','September','October','November','December'],
          weekdays      : ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'],
          weekdaysShort : ['日','一','二','三','四','五','六']
        }
      }
    },
    {
      editor: SelectEditor,
      selectOptions: ["A", "B", "C"],
    },
    {
      editor: TextEditor,
    },
    {
      type: 'custom'
    },
    {
      type: 'numeric',
      numericFormat: {
        pattern: '$0,0.00',
        culture: 'en-US', // this is the default culture, set up for USD
      },
    },
    {

    },
    {}
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

<style>
.htSelectEditor {
  /*
   * This hack enables to change <select> dimensions in WebKit browsers
   */
  -webkit-appearance: menulist-button !important;
  -moz-appearance: menulist-button !important;
  appearance: menulist-button !important;
  position: absolute;
  width: auto;
  z-index: 300;
}
</style>