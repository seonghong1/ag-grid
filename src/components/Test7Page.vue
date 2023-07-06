<template>
  <div style="height: 100%">
    <AgGridVue
      style="width: 1000px; height: 1000px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :getContextMenuItems="getContextMenuItems"
      :allowContextMenuWithControlKey="true"
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
  { headerName: '명세일자', field: 'TRANS_DATE', filter: 'agSetColumnFilter' },
  { headerName: '명세번호', field: 'TRANS_SEQ', filter: 'agSetColumnFilter' },
  { headerName: '매입일자', field: 'WORK_DATE', filter: 'agSetColumnFilter' },
  {
    headerName: '매입구분',
    field: 'WORK_TYPE_NM',
    filter: 'agSetColumnFilter',
  },
  { headerName: '창고이름', field: 'STOCK_NM', filter: 'agSetColumnFilter' },
];

const rowData = dummy_data;

const getContextMenuItems = (params: any) => {
  const result = [
    {
      // custom item
      name: 'Alert ' + params.value,
      action: () => {
        window.alert('Alerting about ' + params.value);
      },
      cssClasses: ['redFont', 'bold'],
    },
    {
      name: 'Country',
      subMenu: [
        {
          name: 'Ireland',
          action: () => {
            console.log('Ireland was pressed');
          },
        },
        {
          name: 'UK',
          action: () => {
            console.log('UK was pressed');
          },
        },
        {
          name: 'France',
          action: () => {
            console.log('France was pressed');
          },
        },
      ],
    },
    {
      name: 'Person',
      subMenu: [
        {
          name: 'Niall',
          action: () => {
            console.log('Niall was pressed');
          },
        },
        {
          name: 'Sean',
          action: () => {
            console.log('Sean was pressed');
          },
        },
        {
          name: 'John',
          action: () => {
            console.log('John was pressed');
          },
        },
        {
          name: 'Alberto',
          action: () => {
            console.log('Alberto was pressed');
          },
        },
        {
          name: 'Tony',
          action: () => {
            console.log('Tony was pressed');
          },
        },
        {
          name: 'Andrew',
          action: () => {
            console.log('Andrew was pressed');
          },
        },
        {
          name: 'Kev',
          action: () => {
            console.log('Kev was pressed');
          },
        },
        {
          name: 'Will',
          action: () => {
            console.log('Will was pressed');
          },
        },
        {
          name: 'Armaan',
          action: () => {
            console.log('Armaan was pressed');
          },
        },
      ],
    },
    'separator',
    {
      // custom item
      name: 'Windows',
      shortcut: 'Alt + W',
      action: () => {
        console.log('Windows Item Selected');
      },
      icon: '<img src="https://www.ag-grid.com/example-assets/skills/windows.png" />',
    },
    {
      // custom item
      name: 'Mac',
      shortcut: 'Alt + M',
      action: () => {
        console.log('Mac Item Selected');
      },
      icon: '<img src="https://www.ag-grid.com/example-assets/skills/mac.png"/>',
    },
    'separator',
    {
      // custom item
      name: 'Checked',
      checked: true,
      action: () => {
        console.log('Checked Selected');
      },
      icon: '<img src="https://www.ag-grid.com/example-assets/skills/mac.png"/>',
    },
    'copy',
    'separator',
    'chartRange',
  ];

  return result;
};
</script>

<style scoped></style>
