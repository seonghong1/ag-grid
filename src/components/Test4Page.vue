<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 1000px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import { dummy_data } from '../../dummy.js';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

const columnDefs = [
  { headerName: '명세일자', field: 'TRANS_DATE', sortable: true },
  { headerName: '명세번호', field: 'TRANS_SEQ', sortable: true },
  { headerName: '매입일자', field: 'WORK_DATE' },
  { headerName: '매입구분', field: 'WORK_TYPE_NM' },
  { headerName: '창고이름', field: 'STOCK_NM' },
];

const rowData = dummy_data;
</script>

<style scoped></style>
