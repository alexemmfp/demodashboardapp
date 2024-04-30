<template>
  <div>
    <h1>{{ title }}</h1>
    <DataTable :value="rows">
      <Column field="name" header="Nombre" sortable filter></Column>
      <Column field="detail" header="Detalle" sortable filter></Column>
    </DataTable>
  </div>
</template>
  
<script>
import DataTable from 'primevue/datatable';
import Column from 'primevue/column';

export default {
  components: {
    DataTable,
    Column
  },
  props: ['title', 'rows'],
};
</script>