<script>
import moment from 'moment'

export default {
  data() {
    return {
      started: false,
      datum: '',
      uhrzeit: '',
      stichwort: '',
      ort: '',
      einheiten: '',
      bericht: '',
      copycontent: ''
    }
  },
  methods: {
    format_date(value) {
      if (value) {
        return moment(String(value)).format('DD.MM.YYYY')
      }
    },
    set_stichwort(e) {
      console.log(e.target.innerText)

      this.$data.stichwort = e.target.innerText;
    },
    create_example() {
      this.$data.datum = new moment().startOf('month').format("YYYY-MM-DD");
      this.$data.uhrzeit = '10:05';
      this.$data.stichwort = "TH_Baum";
      this.$data.ort = "Veenhusen, Alter Kirchpfad";
      this.$data.einheiten = "FF Veenhusen, Polizei";
      this.$data.bericht = 'Das ist ein Beispiel Einsatzbericht.';
    },
    clear_form() {
      this.$data.datum = '';
      this.$data.uhrzeit = '';
      this.$data.stichwort = '';
      this.$data.ort = '';
      this.$data.einheiten = '';
      this.$data.bericht = '';
    }
  }
}
</script>

<template>
  <div class="container" style="max-width: 900px;">

    <div class="tags">
      <a href="https://github.com/turbopixel/Feuerwehr-Beitrag-Generator" title="Quellcode ansehen" target="_blank" rel="me external" class="tag">Quellcode (github.com)</a>
      <a href="https://www.einsatzprotokoll.com" target="_blank" title="Feuerwehr Einsatzprotokoll" class="tag">www.einsatzprotokoll.com</a>
    </div>

    <section class="section pt-0">

      <h1 class="title is-2">Feuerwehr Beitrag Generator</h1>
      <h2 class="subtitle is-5">Für Social Media Posts</h2>

      <div v-if="this.$data.started === false">

        <div class="content">
          <p>Erstelle ein Social Media Post für Facebook und Instagram für deine Feuerwehr in Sekunden.</p>
          <p>
            Klicke unten auf <em>Starten</em> und fülle das Formular mit den Einsatzdaten aus.
          </p>
          <h5 class="title is-5">Beispiel:</h5>
          <pre>Einsatzbericht
⏰ 01.06.2023 12:05
📟 TH_Baum
🌍 Nisselweg, Stadtmitte
🚒 FF Stadtmitte, Polizei

Das ist ein Beispiel Einsatzbericht.</pre>
        </div>

        <button class="button is-success" @click="this.$data.started = true">Starten</button>
      </div>
      <div v-else>
        <hr>
        <div class="columns is-multiline">
          <div class="column is-12">
            <h3 class="title is-4">Einsatzdaten eingeben <span class="tag is-info is-clickable" @click="create_example">Beispiel generieren</span></h3>

            <div class="field is-grouped">
              <div class="control is-expanded">
                <label for="stichwort" class="label">Stichwort</label>
                <input type="text" class="input" v-model="stichwort" id="stichwort">
                <div class="help">
                  <div class="tags">
                    <span class="tag is-clickable" @click="set_stichwort">BMA</span>
                    <span class="tag is-clickable" @click="set_stichwort">TH_VU</span>
                    <span class="tag is-clickable" @click="set_stichwort">TH_Baum</span>
                    <span class="tag is-clickable" @click="set_stichwort">F_HAUS</span>
                    <span class="tag is-clickable" @click="set_stichwort">F_PKW</span>
                  </div>
                </div>
              </div>
              <div class="field is-grouped">
                <div class="control">
                  <label for="datum" class="label">Datum</label>
                  <input type="date" v-model="datum" class="input" id="datum">
                </div>
                <div class="control">
                  <label for="uhrzeit" class="label">Uhrzeit</label>
                  <input type="time" v-model="uhrzeit" class="input" id="uhrzeit">
                </div>
              </div>
            </div>

            <div class="field is-grouped">
              <div class="control is-expanded">
                <label for="ort" class="label">Ort</label>
                <input type="text" class="input" v-model="ort" id="ort">
              </div>
              <div class="control is-expanded">
                <label for="einheiten" class="label">Einheiten vor Ort</label>
                <input type="text" class="input" v-model="einheiten" id="einheiten">
              </div>
            </div>

            <div class="field">
              <label for="bericht" class="label">Einsatzbericht</label>
              <div class="control">
                <textarea class="textarea" rows="3" v-model="bericht" name="bericht"></textarea>
              </div>
            </div>

            <div class="buttons">
              <a class="button is-outlined is-danger is-fullwidth" @click="clear_form">Formular leeren</a>
            </div>

          </div>

          <div class="column is-12">
            <hr>
            <h3 class="title is-4">Ergebnis:</h3>
            <div class="content">
              <p>Kopiere deinen Social Media Post für Facebook und Instagram:</p>
            </div>
            <div class="textarea is-fullwidth" contenteditable="true" rows="6" id="vorschau">
              <strong>Einsatzbericht<br/></strong>
              <strong v-if="datum">&#x23F0; {{ format_date(datum) }} {{ uhrzeit }}<br/></strong>
              <strong v-if="stichwort">&#x1F4DF; {{ stichwort }}<br/></strong>
              <strong v-if="ort">&#x1F30D; {{ ort }}<br/></strong>
              <strong v-if="einheiten">&#x1F692; {{ einheiten }}<br/></strong>

              <p v-if="bericht.length > 0">{{ bericht }}</p></div>
          </div>

        </div>
      </div>

      <footer>
        <hr>
        <small>Copyright 2023 // Powered by <a href="https://hemk.es" title="Nico Hemkes">@turbopixel</a></small>
      </footer>
    </section>
  </div>
</template>

<style>
html, body{
  background: #fdfdfd;
}
</style>