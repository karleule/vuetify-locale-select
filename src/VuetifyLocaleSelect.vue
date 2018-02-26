<template>    
  <v-select class="pa-0"
            v-bind:items="languageItems"
            v-model="selectedLanguage"
            single-line
            auto
            hide-details>
    <template slot="selection" slot-scope="data">
      <flag :iso="data.item.iso" :size="'2'"></flag>
        <span class="ml-3">
          {{data.item.name}}
        </span>
    </template>
    <template slot="item" slot-scope="data">
        <flag :iso="data.item.iso" :size="'2'"></flag>
          <span class="ml-3">
            {{data.item.name}}
          </span>
    </template>
  </v-select>
</template>

<script>
  import Flag from './components/flag.vue'
  import filter from 'lodash/filter'
  import isNil from 'lodash/isNil'
  import map from 'lodash/map'
  let defaultLocales = {
    'en': {
      name: 'English',
      iso: 'en'
    },
    'de': {
      name: 'Deutsch',
      iso: 'de'
    }
  }
  export default {
    props: ['languages', 'value'],
    data () {
      return {
        selectedLanguage: this.value
      }
    },
    components: {
      Flag
    },
    computed: {
      languageItems () {
        let filteredList = filter(this.languages, (item) => {
          return !isNil(defaultLocales[item])
        })
        return map(filteredList, (item) => {
          return defaultLocales[item]
        })
      }
    },
    watch: {
      selectedLanguage (value) {
        this.$emit('input', value.iso)
      }
    }
}
</script>

