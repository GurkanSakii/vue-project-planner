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
    </div>
  </div>
</template>

<script>
export default {
  props: ["proj"],
};
</script>

<style lang="scss" scoped>
.project {
  background: white;
  padding: 10px 0;

  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;

    .proj-right-row {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .proj-left-row {
      display: flex;

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
        }
      }
    }
  }
}
</style>
