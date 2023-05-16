<script setup lang="ts">
import { HotTable, HotColumn } from "@handsontable/vue3";
import { GridSettings } from "handsontable/settings";
import numbro from "numbro";
import jaJP from "numbro/languages/ja-JP";
import trTR from "numbro/languages/tr-TR";
import { registerAllModules } from "handsontable/registry";
import "handsontable/dist/handsontable.full.min.css";

// register Handsontable's modules
registerAllModules();

// register the languages you need
numbro.registerLanguage(jaJP);
numbro.registerLanguage(trTR);

const formatJP = {
  pattern: "0,0.00 $",
  culture: "ja-JP",
};
const formatTR = {
  pattern: "0,0.00 $",
  culture: "tr-TR",
};
const hotData = ref([
  {
    productName: "Product A",
    JP_price: 1.32,
    TR_price: 100.56,
  },
  {
    productName: "Product B",
    JP_price: 2.22,
    TR_price: 453.5,
  },
  {
    productName: "Product C",
    JP_price: 3.1,
    TR_price: 678.1,
  },
  {
    productName: "Product D",
    JP_price: 3.1,
    TR_price: 678.1,
  },
  {
    productName: "Product E",
    JP_price: 3.1,
    TR_price: 678.1,
  },
]);
const settings: GridSettings = reactive({
  height: "auto",
  licenseKey: "non-commercial-and-evaluation",
  manualColumnMove: true,
  contextMenu: true,
  manualColumnFreeze: true,
  comments: true,
  cell: [
    {
      row: 0,
      col: 0,
      comment: {
        value: "This is a comment",
      },
    },
  ]
});
</script>
<template>
  <div>
    <hot-table :data="hotData" :settings="settings">
      <hot-column title="Product name" data="productName" width="120" read-only="true"></hot-column>
      <hot-column
        title="Price in Japan"
        type="numeric"
        :numeric-format="formatJP"
        data="JP_price"
        width="120"
      ></hot-column>
      <hot-column
        title="Price in Turkey"
        data="TR_price"
        type="numeric"
        :numeric-format="formatTR"
        width="120"
      ></hot-column>
    </hot-table>
  </div>
</template>