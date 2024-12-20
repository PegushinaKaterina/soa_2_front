<template>
  <form @submit.prevent>
    Сортировка
    <div class="inputs">
      <div class="input">
        <pre>Колонка: </pre>
        <my-select
          v-model="sortingStrategy.sortingColumn"
          :options="columnOptions"
        />
      </div>
      <div class="input">
        <pre>Тип:     </pre>
        <my-select
          v-model="sortingStrategy.sortingType"
          :options="typeOptions"
        />
      </div>
      <div class="commandButton">
        <my-button class="my-button" type="button" @click="addSortingStrategy"
          >Добавить
        </my-button>
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
        sortingColumn: "NAME",
      },
      columnOptions: [
        { value: "ID", name: "id" },
        { value: "NAME", name: "Имя" },
        { value: "CREATION_DATE", name: "Дата создания" },
        { value: "ANNUAL_TURNOVER", name: "Годовой оборот" },
        { value: "TYPE", name: "Тип" },
        { value: "OFFICIAL_ADDRESS", name: "Официальный адресс" },
      ],
      typeOptions: [
        { value: "asc", name: "По возрастанию" },
        { value: "desc", name: "По убыванию" },
      ],
    };
  },
  methods: {
    addSortingStrategy() {
      this.$emit(
        "addSortingStrategy",
        JSON.parse(JSON.stringify(this.sortingStrategy))
      );
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
