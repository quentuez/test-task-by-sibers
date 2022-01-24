<template>
  <div class="mainTitle">
    <h1 class="h1 mainTitle__h1">User list</h1>
  </div>

  <div class="searchForm">
    <input
      class="input searchForm__input"
      type="search"
      v-model="search"
      placeholder="Search user.."
    />
  </div>

  <div class="listOfUsers" v-for="user in filteredList" :key="user.id">
    <ul class="ul listOfUsers__ul">
      <li class="li ListOfUsers__li">{{ user.name }}</li>
      <li class="li ListOfUsers__li">Number: {{ user.phone }}</li>
    </ul>
    <input
      class="input ListOfUsers__input"
      type="image"
      :src="image"
      alt="Submit"
      width="64"
      height="64"
    />
  </div>
</template>

<script>
export default {
  name: "ContactList",
  data() {
    return {
      // Contact icon created by Creatype - https://www.flaticon.com/premium-icon/writing_3178451
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

<style lang="scss">
.mainTitle {
  background-color: #e48e66;
}

.h1 {
  text-align: center;
}

.input[type="search"] {
  background-color: #f5f5f6;
}

.listOfUsers {
  background: {
    color: #f5f5f6;
  }
}

.ul {
  list-style-type: none;
}

.listOfUsers__ul {
  margin: 25px;
}

.input[type="image"] {
  transition: 0.25s;
  &:hover {
    transition: 0.25s;
    // Filter generated from https://codepen.io/sosuke/pen/Pjoqqp
    filter: invert(63%) sepia(91%) saturate(404%) hue-rotate(322deg)
      brightness(95%) contrast(87%);
  }
}
</style>
