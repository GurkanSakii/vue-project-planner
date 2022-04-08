<template>
  <div class="project">
    <div class="actions">
      <div class="proj-left-row">
        <img src="../../assets/location.svg" />
        <div class="proj-left-area">
          <span>{{ proj.City }}</span>
          <span>{{ proj.Country }}</span>
        </div>
      </div>
      <div class="proj-right-row">
        <span>{{ proj.namesurname }}</span>
        <span>{{ proj.Date }}</span>
      </div>
    </div>
    <div class="data-border"></div>
  </div>
</template>

<script>
export default {
  props: ["proj"],
};
</script>

<style lang="scss" scoped>
.project {
  .actions {
    display: flex;
    height: 79px;
    background: #ffffff;
    border-radius: 8px;
    width: 100%;
    align-items: center;
    justify-content: space-between;

    &:hover {
      background: rgba(79, 117, 194, 0.21);
    }

    .proj-left-row {
      display: flex;
      align-items: center;
      height: 100%;
      min-width: 150px;

      img {
        height: fit-content;
        width: fit-content;
        margin-left: 27px;
      }

      .proj-left-area {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        margin-left: 15px;
        overflow: hidden;

        & > span:first-child {
          font-family: "Inter";
          font-style: normal;
          font-weight: 400;
          font-size: 16px;
          line-height: 20px;
          color: #090a0a;
        }

        & > span:last-child {
          font-family: "Inter";
          font-style: normal;
          font-weight: 400;
          font-size: 14px;
          line-height: 16px;
          color: #72777a;
          margin-top: 3px;
        }
      }
    }

    .proj-right-row {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;
      min-width: 150px;
      height: 100%;
      overflow: hidden;

      & > span:first-child {
        font-family: "Inter";
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 20px;
        color: #484848;
      }

      & > span:last-child {
        font-family: "Inter";
        font-style: normal;
        font-weight: 500;
        font-size: 16px;
        line-height: 16px;
        color: #484848;
        margin-top: 3px;
      }
    }
  }
  .data-border {
    height: 1px;
    width: 100%;
    background: #e7e7e7;
    margin: 10px 0;
  }
}
</style>
