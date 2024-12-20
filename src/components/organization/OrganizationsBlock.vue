<template>
  <div class="organizations-block">
    <div class="organizations-block-elem main-elem">
      <organization-table
        :headerOrganization="headerOrganization"
        :organizations="organizations"
        @moreInfo="$emit('moreInfo', $event)"
        @nextPage="nextPage"
        @prevPage="prevPage"
        @updateOrganization="$emit('updateOrganization', $event)"
        @reload="$emit('reload', $event)"
      ></organization-table>
      {{ pager.pageNum }} / {{ pager.totalPages }}
    </div>
    <div class="column">
      <div class="row">
        <div class="organizations-block-elem additional-elem">
          <filter-block
            :filterStrategies="filterStrategies"
            @addFilterStrategy="addFilterStrategy"
            @deleteFilterStrategy="deleteFilterStrategy"
          ></filter-block>
        </div>
        <div class="organizations-block-elem additional-elem">
          <sorting-block
            :sortingStrategies="sortingStrategies"
            @addSortingStrategy="addSortingStrategy"
            @deleteSortingStrategy="deleteSortingStrategy"
          ></sorting-block>
        </div>
      </div>
      <my-button class="my-button" type="button" @click="getOrganizations(1)"
        >обновить данные с учетом заполненных параметров
      </my-button>
    </div>
  </div>
</template>

<script>
import OrganizationTable from "@/components/organization/OrganizationTable.vue";
import FilterBlock from "@/components/filter/FilterBlock.vue";
import SortingBlock from "@/components/sort/SortingBlock.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";
import OrganizationTableRow from "@/components/organization/OrganizationTableRow.vue";

export default {
  components: {
    OrganizationTableRow,
    MyButton,
    SortingBlock,
    FilterBlock,
    OrganizationTable,
  },
  props: {
    headerOrganization: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      organizations: [],
      pager: {
        pageNum: 1,
        totalPages: 0,
      },
      size: 11,
      filterStrategies: [],
      sortingStrategies: [],
    };
  },
  computed: {
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
  mounted() {
    this.getOrganizations(this.pager.pageNum);
  },
  methods: {
    addFilterStrategy(filterStrategy) {
      if (
        this.filterStrategies
          .map((filter) => filter.filterColumn)
          .includes(filterStrategy.filterColumn)
      ) {
        alert(
          "Фильтрация по колонке " +
            this.columnMap[filterStrategy.filterColumn] +
            " уже есть"
        );
      } else {
        this.filterStrategies.push(filterStrategy);
      }
    },
    addSortingStrategy(sortingStrategy) {
      if (
        this.sortingStrategies
          .map((strategy) => strategy.sortingColumn)
          .includes(sortingStrategy.sortingColumn)
      ) {
        alert(
          "Сортировка по колонке " +
            this.columnMap[sortingStrategy.sortingColumn] +
            " уже есть"
        );
      } else {
        this.sortingStrategies.push(sortingStrategy);
      }
    },
    deleteFilterStrategy(filterStrategy) {
      this.filterStrategies = this.filterStrategies.filter(
        (item) => item !== filterStrategy
      );
    },
    deleteSortingStrategy(sortingStrategy) {
      this.sortingStrategies = this.sortingStrategies.filter(
        (item) => item !== sortingStrategy
      );
    },
    getOrganizations(page = this.pager.pageNum) {
      axios
        .post(
          "https://localhost:8181/organization-service/organizations/search",
          {
            page: page,
            size: this.size,
            sortingStrategies: this.sortingStrategies,
            filterStrategies: this.filterStrategies,
          }
        )
        .then((res) => {
          this.organizations = res.data.organizations;
          this.pager = res.data.pager;
        })
        .catch((error) => alert(error));
    },
    nextPage() {
      if (this.pager.pageNum < this.pager.totalPages) {
        this.getOrganizations(this.pager.pageNum + 1);
      }
    },
    prevPage() {
      if (this.pager.pageNum > 1) {
        this.getOrganizations(this.pager.pageNum - 1);
      }
    },
  },
};
</script>

<style scoped>
.organizations-block {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.organizations-block-elem {
  margin-left: 5px;
  margin-right: 5px;
}

.main-elem {
  width: 59%;
  height: 100%;
  border: black solid 1.5px;
  padding: 10px;
}

.additional-elem {
  width: 49%;
  height: 100%;
}

.row {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: row;
}

.column {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.my-button {
  width: 98%;
  margin: 1%;
}
</style>
