<template>
  <div id="app">
    <photo-stack :covers="covers" title="ねこ" :size="100" :shuffle="true" :deviation="45"></photo-stack>
  </div>
</template>

<script>
  import PhotoStack from './PhotoStack.vue'

  export default {
    name: 'app',
    components: {
      PhotoStack
    },
    data() {
      return {
        covers: ['https://placekitten.com/400/200',
          'https://placekitten.com/200/300',
          'https://placekitten.com/300/200',
          'https://placekitten.com/200/400'
        ]
      }
    }
  }
</script>

<style>
  body {
    background-color: #000;
    font-family: sans-serif;
  }
</style>