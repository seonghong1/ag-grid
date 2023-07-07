<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 500px"
      class="ag-theme-alpine"
      :gridOptions="gridOptions"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import { dummy_data } from '../../dummy.js';

import {
  GridOptions,
  RowSpanParams,
  CellClassParams,
  ColDef,
} from 'ag-grid-community';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

const columnDefs: ColDef[] = [
  {
    headerName: '명세일자',
    field: 'TRANS_DATE',
    rowSpan: rowSpan,
    cellClassRules: {
      'cell-span': (params: CellClassParams) => params.node.rowIndex === 0,
    },
  },
  { headerName: '명세번호', field: 'TRANS_SEQ' },
  {
    headerName: '매입일자',
    field: 'WORK_DATE',
  },
  { headerName: '매입구분', field: 'WORK_TYPE_NM' },
  { headerName: '창고이름', field: 'STOCK_NM' },
];

const rowData = dummy_data;

const gridOptions: GridOptions = {
  columnDefs,
  rowData,
  suppressRowTransform: true,
};

const countByDate = {};

dummy_data.forEach((item, index) => {
  const { TRANS_DATE } = item;
  if (!countByDate[TRANS_DATE]) {
    countByDate[TRANS_DATE] = {
      count: 0,
      startIndex: index,
    };
  }
  countByDate[TRANS_DATE].count++;
});

console.log(countByDate);

function rowSpan(params: RowSpanParams) {
  // if (params.node?.rowIndex === 0) {
  //   return 34;
  // }

  console.log(params.node);

  return 1;
}
</script>

<style scoped></style>
