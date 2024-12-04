<template>
  <div class="tt">
    <sorting-table-header />
    <sorting-table-row
      class="tableRow"
      v-for="sortingStrategy in sortingStrategies"
      :key="sortingStrategy.id"
      :sorting-strategy="sortingStrategy"
      @deleteSortingStrategy="$emit('deleteSortingStrategy', $event)"
    />
  </div>
</template>

<script>
import SortingTableHeader from "@/components/sort/SortingTableHeader.vue";
import SortingTableRow from "@/components/sort/SortingTableRow.vue";
import FilterTableRow from "@/components/filter/FilterTableRow.vue";

export default {
  components: {
    FilterTableRow,
    SortingTableRow,
    SortingTableHeader,
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
.tt {
  height: 100%;
}

.a {
  height: 100%;
  overflow-y: scroll;
  position: relative;
  border: black solid 1.5px;
  padding: 10px;
}

.dotTableHeader {
  background-color: #828670;
  border: 1.5px solid black;
  padding: 10px 0px 10px 0px;
  margin-bottom: 10px;
}

.dotTableHeader :deep(div) {
  background-color: #828670;
  color: black;
}

.closeButton {
  margin: 5px;
  padding: 0;
  width: 20px;
  height: 20px;
  position: absolute;
  top: 0;
  right: 0;
}
.header {
  padding: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}
</style>
