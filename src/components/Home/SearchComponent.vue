<template>
  <div class="home">
    <div>
      <div class="search-bar">
        <div class="searchbar-inner">
          <div class="title">Find in records</div>
          <div class="search-row">
            <div class="search-area">
              <img src="../../assets/search-icon.svg" />
              <input
                type="text"
                v-model="$store.state.search"
                placeholder="Search title.."
              />
            </div>
            <div class="search-button">
              <router-link :to="{ name: 'Results' }">Search</router-link>
            </div>
          </div>
        </div>
      </div>
      <div class="search-results" v-if="$store.state.search">
        <div
          v-for="project in displayedUsers.slice(0, 3)"
          :key="project.id"
          class="project-row"
        >
          <SingleProject :proj="project" />
        </div>

        <div class="showmore" v-if="displayedUsers.length >= 3">
          <router-link :to="{ name: 'Results' }">Show more...</router-link>
        </div>

        <div v-if="displayedUsers.length == 0" class="notfound">
          Data is not found.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../Home/SingleProject.vue";
export default {
  name: "SearchComponent",
  components: {
    SingleProject,
  },
  data() {
    return {
      projects: [],
      search: "",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err));
  },
  computed: {
    displayedUsers() {
      return this.projects.filter((post) => {
        return post.namesurname
          .toLowerCase()
          .includes(this.$store.state.search.toLowerCase());
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  max-width: 800px;
  margin: 0 auto;

  .search-bar {
    display: flex;
    justify-content: center;
    margin-left: 50px;

    .searchbar-inner {
      width: 100%;
    }
  }
  .search-results {
    max-width: 712px;
    height: 248px;
    background: #ffffff;
    border: 1px solid #484848;
    box-sizing: border-box;
    border-radius: 24px;
    padding: 18px 37px;
    margin-top: 17px;
    overflow: auto;

    .project-row {
      position: relative;

      &::after {
        content: "";
        display: block;
        position: absolute;
        bottom: 0;
        width: 90%;
        border-bottom: 1px solid #ddd;
        left: 50%;
        transform: translate(-50%);
      }

      &:nth-last-child(-n + 2)::after {
        border-bottom: none;
      }
    }

    .showmore {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 50px;
      a {
        font-family: "Inter";
        font-style: normal;
        font-weight: 700;
        font-size: 16px;
        line-height: 24px;
        text-decoration: none;
        color: #090a0a;

        &:hover{
          text-decoration: underline;
        }
      }
    }

    .notfound {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
    }
  }

  .title {
    font-family: Inter;
    font-style: normal;
    font-weight: 700;
    color: rgb(9, 10, 10);
    font-size: 32px;
    line-height: 36px;
  }
  .search-row {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: flex-end;
    margin-top: 8px;
  }
  .search-area {
    position: relative;
    width: 100%;

    img {
      position: absolute;
      top: 50%;
      left: 10px;
      transform: translateY(-50%);
    }

    input {
      background: rgb(255, 255, 255);
      padding: 14px;
      border: 2px solid rgb(32, 64, 128);
      border-radius: 8px;
      width: 100%;
      text-indent: 20px;
    }
  }
  .search-button a {
    width: 138px;
    height: 47px;
    border: none;
    margin-left: 11px;
    background: rgb(32, 64, 128);
    font-family: Roboto;
    font-style: normal;
    font-weight: 700;
    text-decoration: none;
    font-size: 18px;
    line-height: 21px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: rgb(255, 255, 255);
    border-radius: 12px;

    &:hover {
      background: #4f75c2;
    }
  }
}
</style>
