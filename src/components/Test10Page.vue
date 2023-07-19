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
//enableRangeSelection - 셀 드레그 후 커맨드 + 클릭으로 원하는 셀만 제거 가능
// copyHeadersToClipboard - 셀 클릭후 복사시 컬럼명까지 복사됨
// editable - 값변경 가능 여부 default: false
// cellEditorPopup - 편집기가 작은 팝업으로 생성됨
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
    editable: true,
    cellEditorPopup: true,
  },
  { headerName: "명세번호", field: "TRANS_SEQ", editable: false },
  { headerName: "매입일자", field: "WORK_DATE", editable: true },
  {
    headerName: "매입구분",
    field: "WORK_TYPE_NM",
    editable: true,
  },
  { headerName: "창고이름", field: "STOCK_NM", editable: true },
  { headerName: "창고이름", field: "STOCK_NM", editable: true },
  { headerName: "창고이름", field: "STOCK_NM", editable: true },
];

const rowData = dummy_data;
</script>

<style scoped></style>
