<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 500px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :defaultColDef="defaultColDef"
      :pinnedBottomRowData="pinnedBottomRowData"
    />
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from 'ag-grid-vue3';
import { onMounted } from 'vue';
import 'ag-grid-enterprise';
import { LicenseManager } from 'ag-grid-enterprise';

import { dummy_data } from '../../dummy';
import { KEY } from '../../key';

import 'ag-grid-community/styles/ag-grid.css';
import 'ag-grid-community/styles/ag-theme-alpine.css';

LicenseManager.setLicenseKey(KEY);

const columnDefs = [
  { headerName: '명세일자', field: 'TRANS_DATE', filter: 'agSetColumnFilter' },

  { headerName: '매입일자', field: 'WORK_DATE', filter: 'agSetColumnFilter' },
  {
    headerName: '매입구분',
    field: 'WORK_TYPE_NM',
    filter: 'agSetColumnFilter',
  },
  { headerName: '창고이름', field: 'STOCK_NM', filter: 'agSetColumnFilter' },
  {
    headerName: '명세번호',
    field: 'TRANS_SEQ',
    filter: 'agSetColumnFilter',
    aggFunc: 'sum',
  },
];

const defaultColDef = {
  flex: 1,
  minWidth: 150,
  sortable: true,
  resizable: true,
};

const rowData = dummy_data;
const createData = (prefix: string) => {
  const result = [
    {
      TRANS_DATE: prefix,
      TRANS_SEQ: dummy_data.length,
    },
  ];

  return result;
};

const pinnedBottomRowData = createData('합계');

onMounted(() => {});
</script>

<style scoped></style>
