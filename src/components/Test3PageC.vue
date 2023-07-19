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
import { AgGridVue } from "ag-grid-vue3";
import { dummy_data } from "../../dummy.ts";

import {
  GridOptions,
  RowSpanParams,
  CellClassParams,
  ColDef,
} from "ag-grid-community";

import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import { GridReadyEvent } from "ag-grid-community";

const countByDate = {};

dummy_data.forEach(({ TRANS_DATE }, index) => {
  if (!countByDate[TRANS_DATE]) {
    countByDate[TRANS_DATE] = {
      data: TRANS_DATE,
      count: 0,
      startIndex: index,
    };
  }
  console.log(countByDate[TRANS_DATE], countByDate[TRANS_DATE].count);
  countByDate[TRANS_DATE].count++;
});

const columnDefs: ColDef[] = [
  {
    headerName: "명세일자",
    field: "TRANS_DATE",
    rowSpan: grid.forEachReow,
    cellClassRules: {
      "cell-span": (params: CellClassParams) => {
        const TRANS_DATE = params.data.TRANS_DATE;

        return (
          TRANS_DATE === countByDate[TRANS_DATE].data &&
          params.node?.rowIndex === countByDate[TRANS_DATE].startIndex
        );
      },
    },
  },
  { headerName: "명세번호", field: "TRANS_SEQ" },
  {
    headerName: "매입일자",
    field: "WORK_DATE",
  },
  { headerName: "매입구분", field: "WORK_TYPE_NM" },
  { headerName: "창고이름", field: "STOCK_NM" },
];

const rowData = dummy_data;

const gridOptions: GridOptions = {
  columnDefs,
  rowData,
  suppressRowTransform: true,
  onGridReady,
};

function onGridReady(params: GridReadyEvent) {
  console.log(params.columnApi.columnModel);
}

function rowSpan(params: RowSpanParams) {
  const TRANS_DATE = params.data.TRANS_DATE;

  // console.log(data);
  // console.log(countByDate[data]);
  if (
    TRANS_DATE === countByDate[TRANS_DATE].data &&
    params.node?.rowIndex === countByDate[TRANS_DATE].startIndex
  ) {
    console.log(countByDate[TRANS_DATE].count);
    return countByDate[TRANS_DATE].count;
  }
}
</script>

<style scoped></style>
