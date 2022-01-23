<template>
  <h1>User list</h1>
  <input type="text" v-model="search" placeholder="Search user.." />
  <ul v-for="user in filteredList" :key="user.id">
    <li>{{ user.name }}</li>
    <li>{{ user.phone }}</li>
  </ul>
</template>

<script>
export default {
  name: "ContactList",
  data() {
    return {
      search: "",
      userList: [],
      // <!-- User list taken from Sibers - https://sibers.ru -->
      usersUrl: "https://demo.sibers.com/users",
    };
  },
  async mounted() {
    let response = await fetch(this.usersUrl);
    if (response.ok) {
      let result = await response.json();
      this.userList = result;
    }
  },
  computed: {
    //[WIP] How to search through multiple parameters (name, phone)?
    filteredList() {
      return this.userList.filter((user) => {
        return (
          user.name.toLowerCase().includes(this.search.toLowerCase()) ||
          user.phone.toLowerCase().includes(this.search.toLowerCase())
        );
      });
    },
  },
};
</script>

<style></style>
