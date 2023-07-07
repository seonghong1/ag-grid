<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 600px"
      class="ag-theme-alpine"
      :gridOptions="gridOptions"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import { dummy_data } from '../../dummy.js';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';
import { GridOptions } from 'ag-grid-community';
import { GridApi } from 'ag-grid-community';
import { ColDef } from 'ag-grid-community';
import { LicenseManager } from 'ag-grid-enterprise';
import { KEY } from '../../key';

LicenseManager.setLicenseKey(KEY);

let gridApi: GridApi | null = null;

const columnDefs: ColDef[] = [
  {
    headerName: '명세일자',
    field: 'TRANS_DATE',
    rowGroup: true,
    hide: true,
  },
  {
    headerName: '명세번호',
    field: 'TRANS_SEQ',
  },
  { headerName: '매입일자', field: 'WORK_DATE' },
  { headerName: '매입구분', field: 'WORK_TYPE_NM' },
  { headerName: '창고이름', field: 'STOCK_NM' },
];

const rowData = dummy_data;

const onGridReady = (params: any) => {
  gridApi = params.api;
};

const gridOptions: GridOptions = {
  columnDefs: columnDefs,
  rowData: rowData,
  onGridReady: onGridReady,
  showOpenedGroup: true,
  groupDisplayType: 'singleColumn',
  autoGroupColumnDef: {
    headerName: '명세일자',
    cellRendererParams: {
      checkbox: true,
    },
  },
  animateRows: true,
  rowSelection: 'multiple',
  groupSelectsChildren: true,
  groupDefaultExpanded: 1,
};
</script>

<style scoped>
.container {
  position: relative;
}
.example-header {
  position: absolute;
  bottom: 15px;
  left: 15px;
}

.ag-header-cell-label {
  justify-content: center;
}
</style>
