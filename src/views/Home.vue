<template>
  <main>
    <nav class="main-nav">
      <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
    </nav>
    <div class="logo-area">
      <div class="logo-inner">
        <img src="../assets/jpg1.jpg" />
        <span class="search">Search App</span>
      </div>
    </div>
    <SearchComponent />
    <SliderComponent />
  </main>

  <FooterComponent />
</template>

<script>
import SearchComponent from "@/components/Home/SearchComponent.vue";
import FooterComponent from "@/components/Home/FooterComponent.vue";
import SliderComponent from "@/components/Home/SliderComponent.vue";
export default {
  name: "Home",
  components: {
    SearchComponent,
    FooterComponent,
    SliderComponent,
  }
};
</script>
<style lang="scss" scoped>
main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 10px;

  .main-nav {
    margin: 64px 62px;
    display: flex;
    justify-content: flex-end;

    a {
      width: 200px;
      height: 46px;
      left: 1020px;
      top: 64px;
      background: #204080;
      border-radius: 12px;
      text-decoration: none;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: "Roboto";
      font-style: normal;
      font-weight: 700;
      font-size: 18px;
      line-height: 21px;
      color: #ffffff;

      &:hover {
        background: #4f75c2;
      }
    }
  }

  .logo-area {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-bottom: 10px;

    .logo-inner {
      display: inline-flex;
      flex-direction: column;

      span {
        position: relative;
        right: -50px;
        font-family: "Roboto";
        font-style: normal;
        font-weight: 700;
        font-size: 18px;
        line-height: 21px;
        text-align: right;
        color: #484848;
        margin-top: 10px;
      }
    }
  }
}
</style>
