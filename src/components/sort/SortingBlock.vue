<template>
  <div class="block">
    <sorting-form
      class="elem form"
      @addSortingStrategy="$emit('addSortingStrategy', $event)"
    ></sorting-form>
    <sorting-table
      :sortingStrategies="sortingStrategies"
      class="elem table"
      @deleteSortingStrategy="$emit('deleteSortingStrategy', $event)"
    ></sorting-table>
  </div>
</template>

<script>
import SortingTable from "@/components/sort/SortingTable.vue";
import SortingForm from "@/components/sort/SortingForm.vue";

export default {
  components: {
    SortingForm,
    SortingTable,
  },
  props: {
    sortingStrategies: {
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
