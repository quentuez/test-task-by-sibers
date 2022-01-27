<template>
  <div class="wrap">
    <div class="mainTitle">
      <h1 class="h1 mainTitle__h1">About app</h1>
    </div>

    <div class="mainInfo wrap__mainInfo">
      <ul class="ul mainInfo__ul">
        <h2>List of used technologies:</h2>
        <li class="li mainInfo__li">HTML5</li>
        <li class="li mainInfo__li">CSS3 / SCSS</li>
        <li class="li mainInfo__li">JavaScript / Vue.js</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutApp",
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
  height: 125px;
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
    width: 1000px;
  }
}

.mainInfo {
  background: {
    color: #f5f5f6;
  }
  border: {
    radius: 5px;
  }
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: 0.3s;
  &:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  }
}

.wrap__mainInfo {
  height: 135px;
  position: relative;
  width: 400px;
  // Small devices (mobiles, 576px and up)
  @media (min-width: 576px) {
    height: 145px;
    width: 500px;
  }
  // Medium devices (tablets, 768px and up)
  @media (min-width: 768px) {
    height: 155px;
    width: 600px;
  }
  // Large devices (desktops, 992px and up)
  @media (min-width: 992px) {
    height: 165px;
    width: 800px;
  }
  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    height: 175px;
    width: 1000px;
  }
}

.ul {
  list-style-type: none;
}

.mainInfo__ul {
  margin: 25px;
  padding-inline-start: 10px;
}
</style>
