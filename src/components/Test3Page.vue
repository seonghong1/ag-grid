<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 500px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :suppressRowTransform="true"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import { dummy_data } from '../../dummy.js';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

const columnDefs = [
  { headerName: '명세일자', field: 'TRANS_DATE' },
  { headerName: '명세번호', field: 'TRANS_SEQ' },
  {
    headerName: '매입일자',
    field: 'WORK_DATE',
    rowSpan: rowSpan,
    cellClassRules: {
      'cell-span': (params: any) =>
        params.data.WORK_DATE === '20230602' && params.node.rowIndex === 0,
    },
  },
  { headerName: '매입구분', field: 'WORK_TYPE_NM' },
  { headerName: '창고이름', field: 'STOCK_NM' },
];

const rowData = dummy_data;

function rowSpan(params: any) {
  console.log(params);
  if (params.data.WORK_DATE === '20230602' && params.node.rowIndex === 0) {
    return 7;
  }

  return 1;
}
</script>

<style scoped></style>
