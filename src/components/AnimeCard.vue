<template>
  <div class="card">
    <a :href="anime.url" target="_blank">
      <img :src="anime.images.jpg.image_url" />
    </a>

    <h3>{{ anime.title }}</h3>
  </div>
</template>

<script>
export default {
  props: ["anime"],
};
</script>

<style lang="scss" scoped>
.card {
  width: 170px;
  height: fit-content;
  margin-bottom: 5%;

  img {
    width: 100%;
    height: 250px;
    border-radius: 15px;
  }
  h3 {
    margin-top: 2%;
    text-align: center;
    color: #FFECEF;
  }

  &:hover {
    transform: scale(1.07);

    h3 {
      color: #FFCACA;
    }
  }
}
</style>