<template>
  <div class="dotTableRow">
    <div class="dotRowElem dotRowNormalElem">
      {{ columnMap[sortingStrategy.sortingColumn] }}
    </div>
    <div class="dotRowElem dotRowNormalElem">
      {{ typeMap[sortingStrategy.sortingType] }}
    </div>
    <div class="dotRowElem dotRowShortElem">
      <my-button
        class="closeButton"
        type="button"
        @click="$emit('deleteSortingStrategy', sortingStrategy)"
      >x</my-button
      >
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {MyButton},
  props: {
    sortingStrategy: {
      type: Object,
      required: true,
    },
  },
  computed: {
    typeMap() {
      return {
        asc: "asc",
        desc: "desc",
      };
    },
    columnMap() {
      return {
        ID: "ID",
        NAME: "NAME",
        CREATION_DATE: "CREATION_DATE",
        ANNUAL_TURNOVER: "ANNUAL_TURNOVER",
        TYPE: "TYPE",
        OFFICIAL_ADDRESS: "OFFICIAL_ADDRESS",
      };
    },
  },
};
</script>

<style scoped>
.dotTableRow {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  color: white;
  text-align: center;
  padding: 10px;
}

.dotRowShortElem {
  width: 5%;
}

.dotRowNormalElem {
  width: 25%;
}

.dotRowLongElem {
  width: 30%;
}
.closeButton {
  margin: 0;
  padding: 0;
  width: 15px;
  height: 15px;
  border-radius: 5px;
}
</style>
