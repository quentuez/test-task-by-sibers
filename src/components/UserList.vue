<template>
  <h1>User list</h1>
  <input type="search" v-model="search" placeholder="Search user.." />
  <div v-for="user in filteredList" :key="user.id">
    <ul>
      <li>{{ user.name }}</li>
      <li>{{ user.phone }}</li>
    </ul>
    <input type="image" :src="image" alt="Submit" width="64" height="64" />
  </div>
</template>

<script>
export default {
  name: "ContactList",
  data() {
    return {
      image: require("@/assets/UserList/EditIcon.png"),
      search: "",
      userList: [],
      // <!-- User list taken from Sibers - https://sibers.ru -->
      usersUrl: "https://demo.sibers.com/users",
    };
  },
  async mounted() {
    let storedUsers = localStorage.getItem("storedUsers");

    if (!storedUsers) {
      await fetch(this.usersUrl)
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            throw new Error("Something went wrong");
          }
        })

        .then((result) => {
          localStorage.setItem("storedUsers", JSON.stringify(result));
        })

        .catch((error) => {
          alert(`There was an error while loading data: [${error}]`);
        });
    }
    this.userList = JSON.parse(localStorage.getItem("storedUsers"));
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
