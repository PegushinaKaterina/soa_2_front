<template>
  <div class="block">
    <filter-form
      class="elem form"
      @addFilterStrategy="$emit('addFilterStrategy', $event)"
    ></filter-form>
    <filter-table
      :filter-strategies="filterStrategies"
      class="elem table"
      @deleteFilterStrategy="$emit('deleteFilterStrategy', $event)"
    ></filter-table>
  </div>
</template>

<script>
import FilterTable from "@/components/filter/FilterTable.vue";
import FilterForm from "@/components/filter/FilterForm.vue";

export default {
  components: {
    FilterForm,
    FilterTable,
  },
  props: {
    filterStrategies: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.block {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.form {
  margin-bottom: 10px;
  height: 280px;
}

.table {
  overflow-y: scroll;
}

.elem {
  width: 100%;
  border: black solid 1.5px;
  padding: 15px;
}
</style>
