<template>
  <div class="result-search-row">
    <div class="result-search-area">
      <input
        type="text"
        :resultsearch="resultsearch"
        placeholder="Search title.."
      />
    </div>
    <div class="result-search-button">
      <button>Search</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      resultsearch: "",
    };
  },
};
</script>

<style lang="scss" scoped>
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
}
</style>
