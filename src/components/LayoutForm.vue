<script>
import moment from 'moment'

export default {
  components: {},
  data() {
    return {
      started: false,
      nummer: '',
      datum: '',
      jahr: '',
      uhrzeit: '',
      dauer: '',
      stichwort: '',
      ort: '',
      einheiten: '',
      bericht: '',
      link: '',
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
    set_datum_uhrzeit(e) {
      console.log(e.target.innerText)

      console.log(new moment().format("HH:mm"))

      this.$data.datum = new moment().format("YYYY-MM-DD");
      this.$data.jahr = new moment().format("YYYY");
      this.$data.uhrzeit = new moment().format("HH:mm");
    },
    set_dauer(e) {
      console.log(e.target.innerText)

      this.$data.dauer = e.target.innerText;
    },
    create_example() {
      this.$data.nummer = "42";
      this.$data.datum = new moment().startOf('month').format("YYYY-MM-DD");
      this.$data.jahr = new moment().format("YYYY");
      this.$data.uhrzeit = new moment().format("HH:mm");
      this.$data.dauer = "1 Stunde";
      this.$data.stichwort = "TH_Baum";
      this.$data.ort = "Veenhusen, Alter Kirchpfad";
      this.$data.einheiten = "FF Veenhusen, Polizei";
      this.$data.bericht = 'Das ist ein Beispiel Einsatzbericht.';
      this.$data.link = 'https://www.einsatzprotokoll.com/einsatzbericht-editor';
    },
    clear_form() {
      this.$data.nummer = '';
      this.$data.datum = '';
      this.$data.jahr = '';
      this.$data.uhrzeit = '';
      this.$data.dauer = '';
      this.$data.stichwort = '';
      this.$data.ort = '';
      this.$data.einheiten = '';
      this.$data.bericht = '';
      this.$data.link = '';
    }
  }
}
</script>

<template>
  <div class="columns is-multiline">
    <div class="column is-12">
      <h3 class="title is-4">Einsatzdaten eingeben <span class="tag is-primary is-clickable" @click="create_example">Beispiel generieren</span></h3>

      <div class="field is-grouped">
        <div class="columns">
          <div class="column is-2">
            <div class="control">
              <label for="nummer" class="label">Nummer</label>
              <input type="text" class="input" v-model="nummer" id="nummer">
            </div>
          </div>
          <div class="column">
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
          </div>
        </div>
      </div>

      <div class="field is-grouped">
        <div class="control">
          <label for="datum" class="label">Datum</label>
          <input type="date" v-model="datum" class="input" id="datum">
          <div class="help">
            <div class="tags">
              <span class="tag is-clickable" @click="set_datum_uhrzeit">Heute</span>
            </div>
          </div>
        </div>
        <div class="control">
          <label for="uhrzeit" class="label">Uhrzeit</label>
          <input type="time" v-model="uhrzeit" class="input" id="uhrzeit">
        </div>
        <div class="control">
          <label for="dauer" class="label">Einsatzdauer</label>
          <input type="text" v-model="dauer" class="input" id="dauer">
          <div class="help">
            <div class="tags">
              <span class="tag is-clickable" @click="set_dauer">0,5 Stunden</span>
              <span class="tag is-clickable" @click="set_dauer">1 Stunde</span>
              <span class="tag is-clickable" @click="set_dauer">1,5 Stunden</span>
              <span class="tag is-clickable" @click="set_dauer">2 Stunden</span>
              <span class="tag is-clickable" @click="set_dauer">2,5 Stunden</span>
              <span class="tag is-clickable" @click="set_dauer">3 Stunden</span>
             </div>
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

      <div class="field">
        <label for="link" class="label">Link zum Beitrag</label>
        <div class="control">
          <input type="text" class="input" v-model="link" name="link"/>
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
        <div v-if="nummer !== '' && jahr !== ''"><strong>&#x1F6A8; +++ Einsatzbericht {{  nummer }} / {{  jahr }} +++</strong></div>
          <div v-else-if="nummer !=='' && jahr === ''"><strong>&#x1F6A8; +++ Einsatzbericht {{ nummer }} +++</strong></div>
          <div v-else><strong>&#x1F6A8; +++ Einsatzbericht +++ </strong></div>
        <strong v-if="datum">&#x23F0; {{ format_date(datum) }} {{ uhrzeit }}<br/></strong>
        <strong v-if="dauer">&#x231B; {{ dauer }}<br/></strong>
        <strong v-if="stichwort">&#x1F4DF; {{ stichwort }}<br/></strong>
        <strong v-if="ort">&#x1F30D; {{ ort }}<br/></strong>
        <strong v-if="einheiten">&#x1F692; {{ einheiten }}<br/></strong>
        <br/>
        <div v-if="bericht.length > 0">{{ bericht }}<br/><br/></div>
        <div v-if="link.length > 0">{{ link }}<br/><br/></div>
        <div>#feuerwehr #112 #einsatzbericht #einsatzinfo #firefighter #ehrenamt</div>
      </div>
    </div>

  </div>
</template>
