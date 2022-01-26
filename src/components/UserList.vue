<template>
  <div class="wrap">
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

    <div
      class="listOfUsers wrap__listOfUsers"
      v-for="user in filteredList"
      :key="user.id"
    >
      <ul id="content" class="ul listOfUsers__ul">
        <li class="li ListOfUsers__li">
          <p>
            <span v-html="user.name" contenteditable="false"></span>
          </p>
        </li>
        <li class="li ListOfUsers__li">
          <p>
            Phone:
            <span v-html="user.phone" contenteditable="false"></span>
          </p>
        </li>
        <li class="li ListOfUsers__li">
          <p>
            Email:
            <span v-html="user.email"></span>
          </p>
        </li>
      </ul>
      <input
        class="input ListOfUsers__input"
        v-on:click="makeEditable"
        type="image"
        :src="image"
        alt="Submit"
        width="32"
        height="32"
      />
      <!-- v-on:click="saveLocalStorage" -->
      <button class="button ListOfUsers__button" type="button">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactList",
  components: {},
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
    // [WIP] How to search through multiple parameters (name, phone)?
    filteredList() {
      return this.userList.filter((user) => {
        return (
          user.name.toLowerCase().includes(this.search.toLowerCase()) ||
          user.phone.toLowerCase().includes(this.search.toLowerCase())
        );
      });
    },
  },
  methods: {
    makeEditable: function () {
      let spans = document.getElementsByTagName("span");
      for (let span of spans) {
        span.setAttribute("contenteditable", true);
      }
    },
    // [WIP] All objects from "storedUsers" are overwritten,
    // but changes should only be made to editable strings.
    saveLocalStorage: function () {
      let content = document.getElementById("content");
      localStorage.setItem("storedUsers", content.innerText);
    },
  },
};
</script>

<style lang="scss">
.mainTitle {
  background: {
    color: #e48e66;
  }
  border: {
    radius: 5px;
  }
}

.h1 {
  text-align: center;
}

.mainTitle__h1 {
  width: 400px;

  // Small devices (mobiles, 576px and up)
  @media (min-width: 576px) {
    width: 500px;
  }

  // Medium devices (tablets, 768px and up)
  @media (min-width: 768px) {
    width: 600px;
  }

  // Large devices (desktops, 992px and up)
  @media (min-width: 992px) {
    width: 800px;
  }

  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    height: 125px;
    width: 1000px;
  }
}

.input[type="search"] {
  background: {
    color: #f5f5f6;
  }
  border: none;
  border: {
    radius: 5px;
  }
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: 0.3s;
  &:focus {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  }
  font: {
    family: "Roboto", sans-serif;
    size: 18px;
    weight: 500;
  }
  outline: none;

  // Small devices (mobiles, 576px and up)
  @media (min-width: 576px) {
    font-size: 21px;
  }

  // Medium devices (tablets, 768px and up)
  @media (min-width: 768px) {
    font-size: 24px;
  }

  // Large devices (desktops, 992px and up)
  @media (min-width: 992px) {
    font-size: 27px;
  }

  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    font-size: 30px;
  }
}

.searchForm__input {
  height: 34px;
  margin-top: 25px;
  width: 100%;

  // Small devices (mobiles, 576px and up)
  @media (min-width: 576px) {
    height: 36px;
  }

  // Medium devices (tablets, 768px and up)
  @media (min-width: 768px) {
    height: 38px;
  }

  // Large devices (desktops, 992px and up)
  @media (min-width: 992px) {
    height: 40px;
  }

  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    height: 42px;
  }
}

.listOfUsers {
  &:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  }
  background: {
    color: #f5f5f6;
  }
  border: {
    radius: 5px;
  }
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: 0.3s;
}

.wrap__listOfUsers {
  height: 85px;
  position: relative;
  width: 400px;

  // Small devices (mobiles, 576px and up)
  @media (min-width: 576px) {
    height: 95px;
    width: 500px;
  }

  // Medium devices (tablets, 768px and up)
  @media (min-width: 768px) {
    height: 105px;
    width: 600px;
  }

  // Large devices (desktops, 992px and up)
  @media (min-width: 992px) {
    height: 115px;
    width: 800px;
  }

  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    height: 125px;
    width: 1000px;
  }
}

.ul {
  list-style-type: none;
}

.listOfUsers__ul {
  margin: 25px;
  padding-inline-start: 10px;
}

.input[type="image"] {
  &:hover {
    // Filter generated from https://codepen.io/sosuke/pen/Pjoqqp
    filter: invert(63%) sepia(91%) saturate(404%) hue-rotate(322deg)
      brightness(95%) contrast(87%);
  }
  transition: 0.3s;
}

.ListOfUsers__input {
  position: absolute;
  top: 15px;
  right: 15px;
}

.button {
  background: {
    color: #63316d;
  }
  color: #f5f5f6;
  border: {
    radius: 5px;
  }

  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: 0.3s;
}

.ListOfUsers__button {
  position: absolute;
  bottom: 15px;
  right: 15px;
}
</style>
