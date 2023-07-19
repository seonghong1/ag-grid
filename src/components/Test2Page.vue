<template>
  <div style="height: 100%">
    <div class="container">
      <AgGridVue
        style="width: 1000px; height: 600px"
        class="ag-theme-alpine"
        :gridOptions="gridOptions"
      />
      <div class="example-header">
        Page Size:
        <select @change="onPageSizeChanged" id="page-size">
          <option value="10">10</option>
          <option value="20">20</option>
          <option value="50">50</option>
          <option value="100">100</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { AgGridVue } from "ag-grid-vue3";
import { dummy_data } from "../../dummy.js";

import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import { GridOptions } from "ag-grid-community";
import { GridApi } from "ag-grid-community";

let gridApi: GridApi | null = null;

const columnDefs = [
  {
    headerName: "명세일자",
    field: "TRANS_DATE",
    sortable: true,
  },
  { headerName: "명세번호", field: "TRANS_SEQ", sortable: true },
  { headerName: "매입일자", field: "WORK_DATE" },
  { headerName: "매입구분", field: "WORK_TYPE_NM" },
  { headerName: "창고이름", field: "STOCK_NM" },
];

const rowData = dummy_data;

const onGridReady = (params: any) => {
  gridApi = params.api;
};

const gridOptions: GridOptions = {
  columnDefs: columnDefs,
  rowData: rowData,
  // 페이징기능
  pagination: true,
  // 페이지당 보여줄 rowdata
  paginationPageSize: 10,
  // 그리드를 동적으로 변화하기 위한 옵션 value
  onGridReady: onGridReady,
};

function onPageSizeChanged(e: Event) {
  const target = e.target as HTMLSelectElement;

  gridApi?.paginationSetPageSize(Number(target.value));
}
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
</style>
