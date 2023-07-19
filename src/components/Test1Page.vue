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
import { AgGridVue } from "ag-grid-vue3";

import { dummy_data } from "../../dummy.js";

import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";

import { GridOptions } from "ag-grid-community";
import { ColDef } from "ag-grid-community";
import { LicenseManager } from "ag-grid-enterprise";

import { KEY } from "../../key";

LicenseManager.setLicenseKey(KEY);

const columnDefs: ColDef[] = [
  {
    headerName: "명세일자",
    field: "TRANS_DATE",
    // autoGroup옵션을 사용하기 때문에 아래 옵션 사용
    rowGroup: true,
    hide: true,
  },
  {
    headerName: "명세번호",
    field: "TRANS_SEQ",
  },
  { headerName: "매입일자", field: "WORK_DATE" },
  { headerName: "매입구분", field: "WORK_TYPE_NM" },
  { headerName: "창고이름", field: "STOCK_NM" },
];

const rowData = dummy_data;

// 컬럼과 데이터는 모두 배열
const gridOptions: GridOptions = {
  // 상단에 노출될 컬럼메뉴들, headerName, field...
  columnDefs: columnDefs,
  // 보여질 데이터들, columnDefs의 field에 해당되는 rowData키들만 노출될거임
  rowData: rowData,
  // 그룹 조건을 로우데이터에 노출시킬지 여부
  showOpenedGroup: true,
  // 레벨에 따른 들여쓰기 여부인듯?
  groupDisplayType: "singleColumn",
  // 해당 컬럼 headerName의 field를 기준으로 그룹핑해줌
  autoGroupColumnDef: {
    headerName: "명세일자",
    cellRendererParams: {
      checkbox: true,
    },
  },
  // transition이 적용되는 거 같음
  animateRows: true,
  // 최상단 체크박스 클릭시 모든 아이템을 선택할건가
  groupSelectsChildren: true,
  // 로우데이터 클릭시 하나만 or 다중선택 , 위의 그룹셀렉티드 옵션을 쓸려면 해당 옵션은 멀티플로
  rowSelection: "multiple",
  // 처음 보여줄 리스트 레벨 / 0루트만, 1루트에서 1레벨, -1모든레벨
  groupDefaultExpanded: 1,
};
</script>

<style scoped>
.container {
}
.example-header {
}

.ag-header-cell-label {
}
</style>
