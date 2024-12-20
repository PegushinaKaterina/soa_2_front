<template>
  <form @submit.prevent>
    Фильтрация
    <div class="inputs">
      <div class="input">
        <pre>Колонка:  </pre>
        <my-select
          v-model="filterStrategy.filterColumn"
          :options="columnOptions"
        />
      </div>
      <div class="input">
        <pre>Тип:      </pre>
        <my-select v-model="filterStrategy.filterType" :options="typeOptions" />
      </div>
      <div class="input">
        <pre>Значение: </pre>
        <my-input v-model="filterStrategy.filterValue" type="text" />
      </div>
      <div class="commandButton">
        <my-button class="my-button" type="button" @click="addFilterStrategy"
          >добавить
        </my-button>
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
        filterColumn: "NAME",
        filterType: "contains",
        filterValue: "",
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
        { value: "contains", name: "Содержит" },
        { value: "more", name: "Больше" },
        { value: "moreOrEquals", name: "Больше или равно" },
        { value: "less", name: "Меньше" },
        { value: "lessOrEquals", name: "Меньше или равно" },
        { value: "equals", name: "Равно" },
      ],
    };
  },
  methods: {
    addFilterStrategy() {
      if (this.filterStrategy.filterValue === "") {
        alert("Значение для фильтрации не может быть пустым");
      } else {
        this.$emit(
          "addFilterStrategy",
          JSON.parse(JSON.stringify(this.filterStrategy))
        );
        this.filterStrategy.id++;
      }
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
