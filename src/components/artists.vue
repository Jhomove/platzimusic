<template>
  <li>
    <h2>
      <div class="card">
        <div class="artista">
          <a :href="artist.url" target="_blank">{{ artist.name }}</a>
        </div>
        <div class="imagen_artista">
          <img :src="artist.image[2]['#text']" alt />
        </div>
      </div>
    </h2>
  </li>
</template>
<script>
export default {
  name: "Artist",
  props: ["artist"]
};
</script>
<style lang="stylus">
li {
  display: block;
  margin: 10px 0;
}
</style>