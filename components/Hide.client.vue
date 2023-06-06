<template>
  <div>
    <hot-table :settings="hotSettings">
    </hot-table>
  </div>
</template>

<script setup lang="ts">
import { HotTable, HotColumn } from "@handsontable/vue3";
import { ContextMenu } from "handsontable/plugins/contextMenu";
import { registerAllModules } from "handsontable/registry";
import "handsontable/dist/handsontable.full.min.css";
import { GridSettings } from "handsontable/settings";
import { HyperFormula } from 'hyperformula';

// register Handsontable's modules
registerAllModules();

const data =   [
    ['A1', '=ROW() & "Second"', '=B1 & "Thrid"', 'D1', '=B1', 'F1', 'G1', 'H1', 'I1', 'J1'],
    ['A2', '=ROW() & "Second"', '=B2 & "Thrid"', 'D2', 'E2', 'F2', 'G2', 'H2', 'I2', 'J2'],
    ['A3', '=ROW() & "Second"', '=B3 & "Thrid"', 'D3', 'E3', 'F3', 'G3', 'H3', 'I3', 'J3'],
    ['A4', '=ROW() & "Second"', '=B4 & "Thrid"', 'D4', 'E4', 'F4', 'G4', 'H4', 'I4', 'J4'],
    ['A5', '=ROW() & "Second"', '=B5 & "Thrid"', 'D5', 'E5', 'F5', 'G5', 'H5', 'I5', 'J5'],
    ['A6', '=ROW() & "Second"', '=B6 & "Thrid"', 'D6', 'E6', 'F6', 'G6', 'H6', 'I6', 'J6'],
  ]
const data2 = [
  {
    productName: "Product A",
    JP_price: 1.32,
    TR_price: 100.56,
    A: '=A1',
    B: '=D1',
  },
  {
    productName: "Product B",
    JP_price: 2.22,
    TR_price: 453.5,
    A: '=A2',
    B: '=D2',
  },
  {
    productName: "Product C",
    JP_price: 3.1,
    TR_price: 678.1,
    A: '=A3',
    B: '=D3',
  },
  {
    productName: "Product D",
    JP_price: 3.1,
    TR_price: 678.1,
    A: '=A4',
    B: '=D4',
  },
  {
    productName: "Product E",
    JP_price: 3.1,
    TR_price: 678.1,
    A: '=A5',
    B: '=D5',
  },
]

// create an external HyperFormula instance
const hyperformulaInstance = HyperFormula.buildEmpty({
  // to use an external HyperFormula instance,
  // initialize it with the `'internal-use-in-handsontable'` license key
  licenseKey: 'internal-use-in-handsontable',
});

const hotSettings: GridSettings = {
  data: data2,
  columns: [
    {
      data: "productName",
      title: "Product",
      readOnly: true,
      // hiddenColumns: true,
    },
    {
      data: "JP_price",
      title: "JP price",
      type: "numeric",
      numericFormat: {
        pattern: "$0,0.00",
      },
    },
    {
      data: "TR_price",
      title: "TR price",
      type: "numeric",
      numericFormat: {
        pattern: "$0,0.00",
      },
    },
    {
      data: "A",
      title: "A",
      type: "numeric",
      numericFormat: {
        pattern: "$0,0.00",
      },
    },
    {
      data: "B",
      title: "B",
      type: "numeric",
      numericFormat: {
        pattern: "$0,0.00",
      },
    }
  ],
  formulas: {
    engine: hyperformulaInstance,
  },
  licenseKey: "non-commercial-and-evaluation",
  colHeaders: true,
  rowHeaders: true,
  height: "auto",
  contextMenu: {
    items: {
      row_above: {
        name: "Insert row above this one (custom name)",
      },
      row_below: {},
      separator: ContextMenu.SEPARATOR,
      clear_custom: {
        name: "Clear all cells (custom)",
      },
    },
  },
  hiddenColumns: {
    columns: [0],
    indicators: true,
  },
};

const columns = [
  {
    title: "First column",
  },
  {
    title: "Second column",
  },
  {
    title: "Third column",
  },
  {
    title: "Fourth column",
  },
  {
    title: "Fifth column",
  },
  {
    title: "Sixth column",
  },
  {
    title: "Seventh column",
  },
  {
    title: "Eighth column",
  },
  {
    title: "Ninth column",
  },
  {
    title: "Tenth column",
  },
  {
    title: "Eleventh column",
  },
];
</script>
