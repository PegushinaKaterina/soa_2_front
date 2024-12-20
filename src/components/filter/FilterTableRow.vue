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
        contains: "содержит",
        more: "больше",
        moreOrEquals: "больше или равно",
        less: "меньше",
        lessOrEquals: "меньше или равно",
        equals: "равно",
      };
    },
    columnMap() {
      return {
        ID: "id",
        NAME: "имя",
        CREATION_DATE: "дата создания",
        ANNUAL_TURNOVER: "годовой оборот",
        TYPE: "тип",
        OFFICIAL_ADDRESS: "официальный адрес",
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

.closeButton {
  margin: 0;
  padding: 0;
  width: 15px;
  height: 15px;
  border-radius: 5px;
}
</style>
