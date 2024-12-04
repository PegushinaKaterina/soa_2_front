<template>
  <div class="organizations-block">
    <div class="organizations-block-elem main-elem">
      <organization-table
        :organizations="organizations"
        :headerOrganization="headerOrganization"
        @moreInfo="$emit('moreInfo', $event)"
        @nextPage="nextPage"
        @prevPage="prevPage"
        @updateOrganization="$emit('updateOrganization', $event)"
      ></organization-table>
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
            @addSortingStrategy="addSortingStrategy"
            @deleteSortingStrategy="deleteSortingStrategy"
            :sortingStrategies="sortingStrategies"
          ></sorting-block>
        </div>
      </div>
      <my-button type="button" @click="getOrganizations" class="my-button"
        >обновить данные с учетом заполненных параметров</my-button
      >
    </div>
  </div>
</template>

<script>
import OrganizationTable from "@/components/organization/OrganizationTable.vue";
import FilterBlock from "@/components/filter/FilterBlock.vue";
import SortingBlock from "@/components/sort/SortingBlock.vue";
import MyButton from "@/components/UI/MyButton.vue";
import axios from "axios";

export default {
  components: {
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
      page: 1,
      size: 4,
      filterStrategies: [],
      sortingStrategies: [],
    };
  },
  mounted() {
    this.getOrganizations();
  },
  methods: {
    addFilterStrategy(filterStrategy) {
      console.log(filterStrategy);
      this.filterStrategies.push(filterStrategy);
    },
    addSortingStrategy(sortingStrategy) {
      console.log(sortingStrategy);
      this.sortingStrategies.push(sortingStrategy);
      console.log(this.sortingStrategies);
    },
    deleteFilterStrategy(filterStrategy) {
      console.log(filterStrategy);
      this.filterStrategies = this.filterStrategies.filter(
        (item) => item !== filterStrategy
      );
    },
    deleteSortingStrategy(sortingStrategy) {
      console.log(sortingStrategy);
      this.sortingStrategies = this.sortingStrategies.filter(
        (item) => item !== sortingStrategy
      );
    },
    getOrganizations() {
      console.log("getOrganizations");
      axios
        .post(
          "https://localhost:8181/organization-service/organizations/search",
          {
            page: this.page,
            size: this.size,
            sortingStrategies: this.sortingStrategies,
            filterStrategies: this.filterStrategies,
          }
        )
        .then((res) => {
          this.organizations = res.data.organizations;
        })
        .catch((error) => console.log(error));
    },
    nextPage() {
      if (this.organizations.length > 0) {
        this.page++;
        this.getOrganizations();
      }
    },
    prevPage() {
      if (this.page > 1) {
        this.page--;
        this.getOrganizations();
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
