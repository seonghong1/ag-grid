<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 1000px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :enableRangeSelection="true"
      :copyHeadersToClipboard="true"
      :suppressRowClickSelection="true"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from "ag-grid-vue3";
import "ag-grid-enterprise";
import { LicenseManager } from "ag-grid-enterprise";

import { dummy_data } from "../../dummy";
import { KEY } from "../../key";

import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";

LicenseManager.setLicenseKey(KEY);

const columnDefs = [
  {
    headerName: "명세일자",
    field: "TRANS_DATE",
    headerCheckboxSelection: true,
    checkboxSelection: true,
  },
  {
    headerName: "명세번호",
    field: "TRANS_SEQ",
    editable: true,
    cellClassRules: {
      "invalid-value": (params: any) => params.value === "1",
    },
  },
  { headerName: "매입일자", field: "WORK_DATE" },
  {
    headerName: "매입구분",
    field: "WORK_TYPE_NM",
  },
  { headerName: "창고이름", field: "STOCK_NM" },
  { headerName: "창고이름", field: "STOCK_NM" },
  { headerName: "창고이름", field: "STOCK_NM" },
];

const rowData = dummy_data;
</script>

<style>
.ag-theme-alpine {
  --ag-selected-row-background-color: lightblue;
}
.ag-row-hover {
  background-color: yellow;
}

.ag-row-focus {
  background-color: antiquewhite;
}

.invalid-value {
  background-color: red;
  color: white;
}
</style>
