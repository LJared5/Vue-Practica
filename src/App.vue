<script lang= "js" setup>
  import DataTable from './components/DataTable.vue'
</script>

<template>
    <header>
      <h1> Tabla De Datos</h1>
    </header>
      <DataTable />

</template>

<style scoped>
  header {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  header h1 {
    font-size: 36px;
  }

</style>
