<template>
  <div class="slider-content">
    <div class="slider-title">Top News</div>
    <div class="slider-area">
      <div class="slider-left-arrow" @click="prevImage">
        <img src="../../assets/slider-arrow.svg" />
      </div>
      <div class="slider-row menu">
        <div v-for="slider in sliders" :key="slider.id">
          <img :src="slider.image" />
          <span class="slider-img-title">{{ slider.title }}</span>
          <span class="slider-img-date">{{ slider.date }}</span>
        </div>
      </div>
      <div class="slider-right-arrow" @click="nextImage">
        <img src="../../assets/slider-arrow.svg" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      scrollAmount: 0,

      sliders: [
        {
          id: 1,
          image: require("../../assets/slider.svg"),
          title: "A Plan to Rebuild the Bus Terminal Everyone Loves to Hate",
          date: "1h ago - by Troy Corlson",
        },
        {
          id: 2,
          image: require("../../assets/slider.svg"),
          title: "A Plan to Rebuild the Bus Terminal Everyone Loves to Hate",
          date: "1h ago - by Troy Corlson",
        },
        {
          id: 3,
          image: require("../../assets/slider.svg"),
          title: "A Plan to Rebuild the Bus Terminal Everyone Loves to Hate",
          date: "1h ago - by Troy Corlson",
        },
        {
          id: 4,
          image: require("../../assets/slider.svg"),
          title: "A Plan to Rebuild the Bus Terminal Everyone Loves to Hate",
          date: "1h ago - by Troy Corlson",
        },
      ],
    };
  },
  methods: {
    nextImage() {
      document.querySelector(".menu").scrollTo({
        left: 400,
        behavior: "smooth",
      });
    },
    prevImage() {
      document.querySelector(".menu").scrollTo({
        left: 0,
        behavior: "smooth",
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.slider-content {
  padding: 100px 0 58px 0;

  .slider-title {
    font-family: "Inter";
    font-style: normal;
    font-weight: 700;
    font-size: 32px;
    line-height: 36px;
    color: #090a0a;
    margin-bottom: 49px;
    margin-left: 55px;
  }

  .slider-area {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;

    .slider-left-arrow {
      display: flex;
      justify-content: center;
      align-items: center;
      min-width: 48px;
      height: 48px;
      background: #eeeeee;
      border-radius: 24px;
      margin-right: 24px;

      &:hover {
        cursor: pointer;
      }
    }
    .slider-right-arrow {
      display: flex;
      justify-content: center;
      align-items: center;
      min-width: 48px;
      height: 48px;
      background: #eeeeee;
      border-radius: 24px;
      transform: rotate(180deg);
      margin-left: 24px;

      &:hover {
        cursor: pointer;
      }
    }

    .slider-row {
      display: flex;
      overflow: auto;
      box-sizing: border-box;
      max-width: 1200px;

      & > div {
        margin-right: 24px;
        display: flex;
        justify-content: center;
        flex-direction: column;

        &:last-child {
          margin-right: 0;
        }
      }
    }

    .slider-img-title {
      font-family: "Inter";
      font-style: normal;
      font-weight: 700;
      font-size: 16px;
      line-height: 24px;
      color: #090a0a;
      margin-top: 12px;
      margin-bottom: 8px;
    }
    .slider-img-date {
      font-family: "Inter";
      font-style: normal;
      font-weight: 400;
      font-size: 12px;
      line-height: 16px;
      color: #6c7072;
    }
  }
}
</style>
