<template>
  <div class="app">
    <div class="header">
      <h2>Добавить организацию</h2>
    </div>
    <div class="main">
      <organization-form class="form appElement" />
    </div>
  </div>
</template>

<script>
import OrganizationForm from "@/components/organization/OrganizationForm.vue";

export default {
  components: {
    OrganizationForm,
  },
  name: "App",
  data() {
    return {
      username: "",
      password: "",
    };
  },
};
</script>

<style scoped>
*:global(*) {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border-radius: 7px;
  background-color: #d7d4c9;
  font-family: "Courier New";
  font-weight: bolder;
  color: black;
}
.app {
  font-size: 15px;
  width: 100%;
  padding: 10px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}
.main {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.form {
  width: 60%;
  height: 60%;
  margin: 10px;
  padding: 20px;
  border: 1px solid black;
  display: flex;
  flex-direction: column;
}

.header {
  width: 100%;
  text-align: center;
  font-size: 30px;
  margin: 50px 0px 50px 0px;
}
</style>
