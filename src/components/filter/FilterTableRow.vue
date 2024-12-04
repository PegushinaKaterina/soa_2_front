<template>
  <div class="dotTableRow">
    <div class="dotRowElem dotRowNormalElem">
      {{ columnMap[filterStrategy.filterColumn] }}
    </div>
    <div class="dotRowElem dotRowNormalElem">
      {{ typeMap[filterStrategy.filterType] }}
    </div>
    <div class="dotRowElem dotRowNormalElem">
      {{ filterStrategy.filterValue }}
    </div>
    <div class="dotRowElem dotRowShortElem">
      <my-button
        class="closeButton"
        type="button"
        @click="$emit('deleteFilterStrategy', filterStrategy)"
        >x
      </my-button>
    </div>
  </div>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: { MyButton },
  props: {
    filterStrategy: {
      type: Object,
      required: true,
    },
  },
  computed: {
    typeMap() {
      return {
        contains: "contains",
        more: "more",
        moreOrEquals: "moreOrEquals",
        less: "less",
        lessOrEquals: "lessOrEquals",
        equals: "equals",
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
