<template>
  <div>
    <section class="hero is-medium is-info">
      <div class="hero-body">
        <div class='columns'>
          <div class='column is-6'>
            <p class="title">
              Large hero
            </p>
            <p class="subtitle">
              Large subtitle
            </p>
          </div>
          <div class='column is-6'>
            <card>
              <template #content="">
                <b-field label='Type de garde'>
                  <b-tooltip
                    type='is-info is-light'
                    label='Je confie mon animal au pet sitter'
                    position='is-bottom'
                  >
                    <b-radio-button v-model="radioButton"
                                    native-value="garde"
                                    type="is-primary is-light is-outlined">
                      <b-icon icon="home"></b-icon>
                      <span>Garde à domicile</span>
                    </b-radio-button>
                  </b-tooltip>

                  <b-tooltip
                    type='is-info is-light'
                    label='Le pet sitter se déplace à mon domicile'
                    position='is-bottom'
                  >
                    <b-radio-button v-model="radioButton"
                                    native-value="visite"
                                    type="is-primary is-light is-outlined">
                      <b-icon icon="run"></b-icon>
                      <span>Visite</span>
                    </b-radio-button>
                  </b-tooltip>
                </b-field>
                <div class='columns'>
                  <div class='column'>
                    <b-field label='Dates'>
                      <b-datepicker
                        ref='datepicker'
                        v-model="dates"
                        locale='fr-FR'
                        placeholder="Séléctionnez les dates"
                        range>
                      </b-datepicker>
                      <b-button
                        icon-left="calendar-today"
                        type="is-primary"
                        @click="$refs.datepicker.toggle()" />
                    </b-field>
                  </div>
                  <div class='column'>
                    <b-field label="Ville">
                      <b-input id='googleSearch' label='ville' placeholder='Indiquez une ville'></b-input>
                    </b-field>
                  </div>
                </div>
                <b-field label="Animal">
                  <b-select v-model='animal' placeholder="Selectionnez un animal" icon='paw'>
                    <option
                      v-for="pet in animals"
                      :key="pet.value"
                      :value="pet.value">
                      {{ pet.text }}
                    </option>
                  </b-select>
                </b-field>
                <b-field label="Nombre d'animaux">
                  <b-numberinput v-model="number"></b-numberinput>
                </b-field>
                <b-field style='text-align: center' class='mt-5'>
                  <b-button :disabled='!valid' label='Rechercher' type='is-primary'></b-button>
                </b-field>
              </template>
            </card>
          </div>
        </div>
      </div>
    </section>
    <section class="container pt-4 is-10">
      <div class="columns is-mobile">
        <card
          title="Free"
          icon="github"
        >
          Open source on <a href="https://github.com/buefy/buefy">
          GitHub check
        </a>
        </card>

        <card
          title="Responsive"
          icon="cellphone-link"
        >
          <b class="has-text-grey">
            Every
          </b> component is responsive
        </card>

        <card
          title="Modern"
          icon="alert-decagram"
        >
          Built with <a href="https://vuejs.org/">
          Vue.js
        </a> and <a href="http://bulma.io/">
          Bulma
        </a>
        </card>

        <card
          title="Lightweight"
          icon="arrange-bring-to-front"
        >
          No other internal dependency
        </card>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'HomePage',
  data() {
    return {
      radioButton: 'visite',
      animals: [
        {
          value: 'cat',
          text: 'Chat'
        },
        {
          value: 'dog',
          text: 'Chien'
        },
        {
          value: 'rabbit',
          text: 'Lapin'
        }
      ],
      animal: null,
      dates: [],
      number: 1,
    }
  },
  head() {
    return {
      title: 'Mokai | Index'
    }
  },
  computed: {
    valid() {
      return this.dates.length > 0 && this.animal !== null
    }
  },
  mounted() {
    // const input = this.$refs.citySearch
    // eslint-disable-next-line no-new,no-undef
    new google.maps.places.Autocomplete(document.getElementById('googleSearch'), {
      types: ['(cities)']
    })
  }
}
</script>
