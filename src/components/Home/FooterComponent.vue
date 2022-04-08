<template>
  <div class="footer-area">
    <img src="../../assets/footer-image.svg" alt="" />
    <div class="contact-area">
      <div>
        <span class="contact">İletişim</span>
        <div>
          Adres: Çifte Havuzlar Mah. Eski Londra Asfaltı Cad. Kuluçka Merkezi D2
          Blok No: 151/1F İç Kapı No: 2B03 Esenler/İstanbul
        </div>
      </div>
      <span class="contact"> Email: bilgi@testodev.com </span>
    </div>
    <Map />
  </div>
</template>

<script>
import Map from "../Home/Map.vue";
export default {
  components: {
    Map,
  },
};
</script>

<style lang="scss" scoped>
.footer-area {
  width: 100%;
  height: 277.13px;
  background: rgba(41, 78, 152, 0.72);
  display: flex;
  padding: 10px;
  box-sizing: border-box;
  padding: 49px 60px;

  .contact-area {
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: space-evenly;
    margin: 0 20px;
    overflow: hidden;
  }
  .contact {
    font-family: "Roboto";
    font-style: normal;
    font-weight: 700;
    font-size: 18px;
    line-height: 21px;
    color: #ffffff;
  }

  div div {
    font-family: "Roboto";
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 21px;
    color: #ffffff;
  }
}
</style>
