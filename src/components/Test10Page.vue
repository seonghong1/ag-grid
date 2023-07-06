<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 1000px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :enableRangeSelection="true"
      :copyHeadersToClipboard="true"
      :rowData="rowData"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import 'ag-grid-enterprise';
import { LicenseManager } from 'ag-grid-enterprise';

import { dummy_data } from '../../dummy';
import { KEY } from '../../key';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

LicenseManager.setLicenseKey(KEY);

const columnDefs = [
  { headerName: '명세일자', field: 'TRANS_DATE', cellEditorPopup: true },
  { headerName: '명세번호', field: 'TRANS_SEQ', editable: true },
  { headerName: '매입일자', field: 'WORK_DATE', editable: true },
  {
    headerName: '매입구분',
    field: 'WORK_TYPE_NM',
    editable: true,
  },
  { headerName: '창고이름', field: 'STOCK_NM', editable: true },
  { headerName: '창고이름', field: 'STOCK_NM', editable: true },
  { headerName: '창고이름', field: 'STOCK_NM', editable: true },
];

const rowData = dummy_data;
</script>

<style scoped></style>
