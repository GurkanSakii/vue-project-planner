<template>
  <div class="results">
    <div class="results-area">
      <img src="../assets/logo2.png" />

      <div class="result-search-row">
        <div class="result-search-area">
          <input
            type="text"
            v-model="$store.state.search"
            placeholder="Search title.."
            @click="getFirstPage()"
          />
        </div>
        <div class="result-search-button">
          <button @click="getFirstPage()">Search</button>
        </div>
      </div>

      <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
    </div>
    <div class="result-area-content">
      <div class="result-projects">
        <div
          v-for="project in displayedUsers"
          :key="project.id"
          class="resultdata-area"
        >
          <ResultData :proj="project" />
        </div>
        <div v-if="displayedUsers.length == 0" class="nodata">Veri yok.</div>
      </div>

      <div class="sort-content">
        <div @click="dropdownOpen" class="sort-select-area">
          <img src="../assets/sorting.png" />
          <span>Order By</span>
        </div>
        <div v-if="opendrop" class="dropdown-open">
          <div class="dropdown-area">
            <div
              v-for="(sortType, index) in sortingTypes"
              @click="sortingData(sortType, index)"
              :key="index"
              :class="{ active: index === activeIndex }"
            >
              <span> {{ sortType }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div>
      <ul class="pagination">
        <li>
          <button @click="page = 1">
            <span>En Başa Dön</span>
          </button>
        </li>
        <li>
          <button v-if="page != 1" @click="page--">
            <span>Bir Önceki</span>
          </button>
        </li>
        <li v-for="pageNumber in pages" :key="pageNumber">
          <button
            @click="page = pageNumber"
            :class="{ active: page === pageNumber }"
          >
            {{ pageNumber }}
          </button>
        </li>
        <li>
          <button @click="page++" v-if="page < pages">
            <span>Bir Sonraki</span>
          </button>
        </li>
        <li>
          <button @click="page = pages">
            <span>En Sona Git</span>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import ResultData from "../components/Results/ResultData.vue";
import SearchComponent from "../components/Home/SearchComponent.vue";
import ResultInput from "../components/Results/ResultInput.vue";
export default {
  name: "Home",
  components: {
    ResultData,
    SearchComponent,
    ResultInput,
  },
  data() {
    return {
      projects: [],
      search: "",
      page: 1,
      perPage: 5,
      pages: null,
      opendrop: false,
      sortingTypes: ["name", "city", "country"],
      activeIndex: null,
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err));
  },
  methods: {
    dropdownOpen() {
      this.opendrop = !this.opendrop;
    },
    setPages(filterpage) {
      if (this.$store.state.search) {
        var numberOfPages = Math.ceil(filterpage / this.perPage);
        this.pages = numberOfPages;
      } else {
        var numberOfPages = Math.ceil(this.projects.length / this.perPage);
        this.pages = numberOfPages;
      }
    },
    getFirstPage() {
      this.page = 1;
    },
    paginate(projects) {
      var page = this.page;
      var perPage = this.perPage;
      var from = page * perPage - perPage;
      var to = page * perPage;
      return projects.slice(from, to);
    },
    sortingData(sort, index) {
      this.activeIndex = index;
      if (sort == "name") {
        this.projects.sort((a, b) => {
          let fa = a.namesurname.toLowerCase(),
            fb = b.namesurname.toLowerCase();

          if (fa < fb) {
            return -1;
          }
          if (fa > fb) {
            return 1;
          }
          return 0;
        });
      }
      if (sort == "city") {
        this.projects.sort((a, b) => {
          let fa = a.City.toLowerCase(),
            fb = b.City.toLowerCase();
          if (fa < fb) {
            return -1;
          }
          if (fa > fb) {
            return 1;
          }
          return 0;
        });
      }
      if (sort == "country") {
        this.projects.sort((a, b) => {
          let fa = a.Country.toLowerCase(),
            fb = b.Country.toLowerCase();

          if (fa < fb) {
            return -1;
          }
          if (fa > fb) {
            return 1;
          }
          return 0;
        });
      }

      return this.projects;
    },
  },
  computed: {
    displayedUsers() {
      let filterproject = this.projects;
      if (this.$store.state.search) {
        filterproject = filterproject.filter((post) => {
          return post.namesurname
            .toLowerCase()
            .includes(this.$store.state.search.toLowerCase());
        });
        this.filterlength = filterproject.length;
      }

      return this.paginate(filterproject);
    },
  },
  watch: {
    displayedUsers() {
      this.setPages(this.filterlength);
    },
  },
};
</script>
<style lang="scss" scoped>
.results {
  padding: 27px 37px;

  .resultdata-area {
    width: 100%;
    margin: 0 auto;
  }
  .sort-content {
    margin-left: 20px;
    display: flex;
    flex-direction: column;
    min-width: 175px;

    .sort-select-area {
      background: #f3f2f2;
      border: 1px solid #414141;
      box-sizing: border-box;
      border-radius: 8px;
      width: 126px;
      height: 30px;
      font-family: "Roboto";
      font-style: normal;
      font-weight: 500;
      font-size: 18px;
      line-height: 21px;
      color: #484848;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 8px;

      &:hover {
        cursor: pointer;
      }
    }
    .dropdown-open {
      background: #ffffff;
      border: 1px solid #8f8f8f;
      box-sizing: border-box;
      box-shadow: 4px 6px 12px 4px rgba(0, 0, 0, 0.2);
      border-radius: 8px;
      width: 156px;
      margin-top: 15px;

      .dropdown-area {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        flex-direction: column;
        padding: 10px;
        height: 100%;
        width: 100%;
        text-transform: capitalize;

        & > .active {
          background: #b3b3b3;
          border-radius: 8px;
          color: #fff;
        }

        & > div {
          margin-bottom: 7px;
          display: flex;
          align-items: center;
          justify-content: flex-start;
          width: 100%;
          height: 30px;
          color: #000000;
          padding: 0 15px;

          &:last-child {
            margin-bottom: 0px;
          }
        }

        span {
          font-family: "Roboto";
          font-style: normal;
          font-weight: 500;
          font-size: 14px;
          line-height: 16px;
        }

        &.active {
          color: red;
        }
      }
    }
  }

  .results-area {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    flex-wrap: wrap;
    margin-bottom: 50px;

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
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-top: 50px;

  .active {
    background: #204080;
    border: 1px solid #ffffff;
    color: #fff;
  }

  li button {
    background: #ffffff;
    border: 1px solid #484848;
    box-sizing: border-box;
    border-radius: 4px;
    min-width: 24px;
    height: 24px;
    margin: 0 5px;
    overflow: hidden;

    span {
      font-family: "Roboto";
      font-style: normal;
      font-weight: 700;
      font-size: 14px;
      padding: 0px 10px;
      color: #484848;
    }
  }
}

.result-search-row {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 50%;
}
.result-search-area {
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
.result-search-button button {
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
    cursor: pointer;
  }
}
.result-area-content {
  display: flex;
  max-width: 1200px;
  margin: auto;
  width: 100%;
  justify-content: center;
  flex-wrap: wrap;

  .result-projects {
    width: 950px;

    .nodata {
      text-align: center;
    }
  }
}
</style>
