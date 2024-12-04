<template>
  <div class="tt">
    <div class="tt-content">
      <organization-table-header
        :organization="headerOrganization"
        class="dotTableHeader"
      />
      <organization-table-row
        class="tableRow"
        v-for="organization in organizations"
        :key="organization.id"
        :organization="organization"
        @moreInfo="$emit('moreInfo', $event)"
        @updateOrganization="$emit('updateOrganization', $event)"
      />
    </div>
    <div class="right">
      <my-button type="button" @click="$emit('prevPage')" class="my-button"
      >предыдущая страница</my-button
      >
      <my-button type="button" @click="$emit('nextPage')" class="my-button"
        >следующая страница</my-button
      >
    </div>
  </div>
</template>

<script>
import OrganizationTableRow from "@/components/organization/OrganizationTableRow.vue";
import OrganizationTableHeader from "@/components/organization/OrganizationTableHeader.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
  components: {
    MyButton,
    OrganizationTableHeader,
    OrganizationTableRow,
  },
  props: {
    organizations: {
      type: Array,
    },
    headerOrganization: {
      type: Object,
    },
  },
  data() {
    return {
      currentOrganization: {
        name: "",
        coordinates: {
          x: 0,
          y: 0,
        },
        annualTurnover: "",
        type: "",
        officialAddress: {
          zipCode: "",
        },
      },
    };
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
.tt-content {
  height: 90%;
}
.right {
  display: flex;
  flex-direction: row;
  justify-content: right;
}
.my-button {
  margin: 5px;
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
