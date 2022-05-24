<template>
  <div>
    <cep-finder-home></cep-finder-home>
  </div>
</template>

<script>
import CepFinderHome from "./views/CepFinderHome.vue";

export default {
  name: "App",
  components: {
    CepFinderHome,
  },
};
</script>

<style> 
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&display=swap");

:root {
  --header-color: #9206e9;
  --purple-color: #b600ee;
  --white-color: #fff;
  --gray-color: #f6f6f6;
  --gray-color-2: #bbc4ce;
  --gray-color-3: #75818c;
  --gray-color-4: #b7b7b7;
  --gray-color-5: #e0e6ea;
  --dark-color: #20272c;
}

html,
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  height: 100vh;
  width: 100%;
  position: relative; 
  font-family: "Open Sans", sans-serif;
}
* {
  margin: 0;
}
</style>
