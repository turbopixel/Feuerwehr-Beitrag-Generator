<script>
import LayoutStart from "./components/LayoutStart.vue";
import LayoutForm from "./components/LayoutForm.vue";

export default {
  components: {LayoutForm, LayoutStart},
  data() {
    return {
      started: false,
    }
  },
}
</script>

<template>
  <div class="container" style="max-width: 900px;">

    <section class="section pt-0">
      <div class="tags mt-2 mb-1">
        <a href="https://www.einsatzprotokoll.com" target="_blank" title="Feuerwehr Einsatzprotokoll" class="tag is-link is-rounded">www.einsatzprotokoll.com</a>
        <a href="https://github.com/turbopixel/Feuerwehr-Beitrag-Generator" title="Quellcode ansehen" target="_blank" rel="me external" class="tag is-info is-rounded">Quellcode (github.com)</a>
      </div>

      <h1 class="title is-2">Feuerwehr Beitrag Generator</h1>
      <h2 class="subtitle is-5">Für Social Media Posts</h2>

      <div v-if="this.$data.started === false">
        <LayoutStart/>
        <button class="button is-success" @click="this.$data.started = true">Post erstellen</button>
        <hr>
        <h1 class="title is-4">Feuerwehr Einsatzprotokoll</h1>
        <p>Kennst du schon das Feuerwehr Einsatzprotokoll? Mit der kostenlosen Software kannst du Einsatzbericht online für deine Feuerwehr verwalten und auch im Team gemeinsam bearbeiten.</p>
        <a href="https://www.einsatzprotokoll.com" target="_blank" rel="external" class="button is-text">www.einsatzprotokoll.com</a>
      </div>
      <div v-else>
        <hr>
        <LayoutForm/>
      </div>

      <footer>
        <hr>
        <small>Copyright 2023-2025 // Powered by <a href="https://hemk.es" rel="noopener me external" target="_blank" title="Nico Hemkes">Nico Hemkes</a></small>
      </footer>
    </section>
  </div>
</template>

<style>
html, body{
  background: #fdfdfd;
}
</style>