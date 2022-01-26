<template class="template">
  <div>
    <router-link class="router-link" to="/">Home</router-link> |
    <router-link class="router-link" to="/aboutapp">About app</router-link>
    <router-view />
  </div>
</template>

<script></script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

.router-link {
  transition: 0.3s;
  text-decoration: none;
  &:visited {
    color: #212121;
  }
  &:hover {
    text-decoration: underline;
    color: #63316d;
  }
}

.body {
  background: {
    color: #e1e2e1;
  }
  color: #212121;
}
.wrap {
  background: {
    color: #e1e2e1;
  }
  font: {
    family: "Roboto", sans-serif;
    size: 18px;
    weight: 500;
  }

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

.body__wrap {
  align-items: center;
  display: flex;
  flex: {
    direction: column;
  }
}

* {
  margin: 0;
}
</style>
