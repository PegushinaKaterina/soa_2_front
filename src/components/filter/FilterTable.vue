<template>
  <div class="tt">
    <filter-table-header />
    <filter-table-row
      v-for="filterStrategy in filterStrategies"
      :key="filterStrategy.id"
      :filterStrategy="filterStrategy"
      class="tableRow"
      @deleteFilterStrategy="$emit('deleteFilterStrategy', $event)"
    />
  </div>
</template>

<script>
import FilterTableRow from "@/components/filter/FilterTableRow.vue";
import FilterTableHeader from "@/components/filter/FilterTableHeader.vue";

export default {
  components: {
    FilterTableHeader,
    FilterTableRow,
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
