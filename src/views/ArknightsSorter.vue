<template>
    <Sorter sorterNameProp="Arknights" imageProp="" :dictionaryObjectProp="ArknightsDictionaryObject"/>
</template>

<script>
// @ is an alias to /src
import Sorter from '@/components/Sorter.vue'
import ArknightsObject from '@/data/arknights_operator.json'

export default {
  name: 'AikatsuSorter',
  components: {
    Sorter
  },
  data() {
    return {
      ArknightsDictionaryObject: {"Arknights": { array: ArknightsObject } }     
    }
  }

}
</script>
