<template>
  <div>
    <hot-table :settings="hotSettings">
      <hot-column v-for="column in columns" :settings="column" />
    </hot-table>
  </div>
</template>

<script setup lang="ts">
import { HotTable, HotColumn } from "@handsontable/vue3";
import { ContextMenu } from "handsontable/plugins/contextMenu";
import { registerAllModules } from "handsontable/registry";
import "handsontable/dist/handsontable.full.min.css";
import { GridSettings } from "handsontable/settings";

// register Handsontable's modules
registerAllModules();

const hotSettings: GridSettings = {
  licenseKey: "non-commercial-and-evaluation",
  data: [
    ["A1", "=ROW()", "C1", "D1", "E1", "F1", "G1", "H1", "I1", "J1"],
    ["A2", "=ROW()", "C2", "D2", "E2", "F2", "G2", "H2", "I2", "J2"],
    ["A3", "=ROW()", "C3", "D3", "E3", "F3", "G3", "H3", "I3", "J3"],
    ["A4", "=ROW()", "C4", "D4", "E4", "F4", "G4", "H4", "I4", "J4"],
    ["A5", "=ROW()", "C5", "D5", "E5", "F5", "G5", "H5", "I5", "J5"],
    ["A6", "=ROW()", "C6", "D6", "E6", "F6", "G6", "H6", "I6", "J6"],
  ],
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
  comments: true,
  // fixedColumnsStart: 1,
  // fixedColumnsLeft: 1,
  // fixedRowsTop: 1,

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
