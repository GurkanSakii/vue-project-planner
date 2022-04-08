<template>
  <div class="googlemap">
    <iframe
      src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d7159.350898377564!2d28.889889110729474!3d41.02227491981687!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x14cabb7abf29ba35%3A0xc98f44e9057adcde!2zVGVzb2RldiBZYXrEsWzEsW0gRG9uYW7EsW0gQmlsacWfaW0gQml5b21lZGlrYWwgS29uZ3JlIFR1cml6bSBFxJ9pdGltIERhbsSxxZ9tYW5sxLFrIExpbWl0ZWQgxZ5pcmtldGk!5e0!3m2!1str!2str!4v1648713090476!5m2!1str!2str"
      allowfullscreen=""
      loading="lazy"
      referrerpolicy="no-referrer-when-downgrade"
    ></iframe>
  </div>
</template>

<script>
export default {
};
</script>

<style lang="scss" scoped>
.googlemap {
  width: 50%;

  iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }
}
</style>
