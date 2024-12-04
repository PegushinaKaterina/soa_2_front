<template>
  <form @submit.prevent>
    <div class="inputs">
      <div class="input">
        <pre>column: </pre>
        <my-select
          v-model="filterStrategy.filterColumn"
          :options="columnOptions"
        />
      </div>
      <div class="input">
        <pre>type:   </pre>
        <my-select v-model="filterStrategy.filterType" :options="typeOptions" />
      </div>
      <div class="input">
        <pre>value:  </pre>
        <my-input v-model="filterStrategy.filterValue" type="text" />
      </div>
      <div class="commandButton">
        <my-button type="button" @click="addFilterStrategy" class="my-button"
          >добавить</my-button
        >
      </div>
    </div>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: { MySelect, MyInput, MyButton },
  data() {
    return {
      filterStrategy: {
        id: 0,
        filterColumn: "ID",
        filterType: "contains",
        filterValue: "",
      },
      columnOptions: [
        { value: "ID", name: "ID" },
        { value: "NAME", name: "NAME" },
        { value: "CREATION_DATE", name: "CREATION_DATE" },
        { value: "ANNUAL_TURNOVER", name: "ANNUAL_TURNOVER" },
        { value: "TYPE", name: "TYPE" },
        { value: "OFFICIAL_ADDRESS", name: "OFFICIAL_ADDRESS" },
      ],
      typeOptions: [
        { value: "contains", name: "contains" },
        { value: "more", name: "more" },
        { value: "moreOrEquals", name: "moreOrEquals" },
        { value: "less", name: "less" },
        { value: "lessOrEquals", name: "lessOrEquals" },
        { value: "equals", name: "equals" },
      ],
    };
  },
  methods: {
    addFilterStrategy() {
      this.$emit(
        "addFilterStrategy",
        JSON.parse(JSON.stringify(this.filterStrategy))
      );
      this.filterStrategy.id++;
    },
  },
};
</script>

<style scoped>
.inputs {
  height: 100%;
  padding: 5px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.input {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

pre {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.my-button {
  width: 100%;
}
</style>
