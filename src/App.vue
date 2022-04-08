<template>
  <router-view />
</template>

<script>
export default {};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Roboto:wght@300;400;500;700;900&display=swap");
html {
  box-sizing: border-box;
}
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}
body {
  background-color: #fcfcfc;
}

#app {
  font-family: 'Roboto', 'Inter', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  color: #2c3e50;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
::-webkit-scrollbar {
  display: none;
}

@font-face {
  font-family: "Roboto";
  font-weight: 300;
  src: url("../src/fonts/Roboto-Light.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Roboto";
  font-weight: 400;
  src: url("../src/fonts/Roboto-Regular.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Roboto";
  font-weight: 500;
  src: url("../src/fonts/Roboto-Medium.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Roboto";
  font-weight: 700;
  src: url("../src/fonts/Roboto-Bold.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Roboto";
  font-weight: 900;
  src: url("../src/fonts/Roboto-Black.woff2") format("woff2");
  font-display: swap;
}

@font-face {
  font-family: "Inter";
  font-weight: 300;
  src: url("../src/fonts/Inter-Light.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Inter";
  font-weight: 400;
  src: url("../src/fonts/Inter-Regular.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Inter";
  font-weight: 500;
  src: url("../src/fonts/Inter-Medium.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Inter";
  font-weight: 600;
  src: url("../src/fonts/Inter-SemiBold.woff2") format("woff2");
  font-display: swap;
}
@font-face {
  font-family: "Inter";
  font-weight: 700;
  src: url("../src/fonts/Inter-Bold.woff2") format("woff2");
  font-display: swap;
}
</style>
