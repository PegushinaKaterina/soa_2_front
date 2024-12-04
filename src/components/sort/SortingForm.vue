<template>
  <form @submit.prevent>
    <div class="inputs">
      <div class="input">
        <pre>column: </pre>
        <my-select
          v-model="sortingStrategy.sortingColumn"
          :options="columnOptions"
        />
      </div>
      <div class="input">
        <pre>type:   </pre>
        <my-select
          v-model="sortingStrategy.sortingType"
          :options="typeOptions"
        />
      </div>
      <div class="commandButton">
        <my-button
          type="button"
          @click="addSortingStrategy"
          class="my-button"
          >добавить</my-button
        >
      </div>
    </div>
  </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MySelect from "@/components/UI/MySelect.vue";

export default {
  components: { MySelect, MyButton },
  data: function () {
    return {
      sortingStrategy: {
        id: 0,
        sortingType: "asc",
        sortingColumn: "ID",
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
        { value: "asc", name: "asc" },
        { value: "desc", name: "desc" },
      ],
    };
  },
  methods: {
    addSortingStrategy() {
      this.$emit(
        "addSortingStrategy",
        JSON.parse(JSON.stringify(this.sortingStrategy))
      );
      this.sortingStrategy.id++;
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
