<template>
      <div class="example-modal-content">
       <center>
        <h1>{{ WEIGHT }}</h1>
        <h1>{{ NOTA_FISCAL }}</h1>
        <h1>{{ LAST_UPD }}</h1>
       </center>
      </div>
</template>
  <script>
  export default {
    name: 'Detalhes.vue',

    props: {
      WEIGHT: String,
      NOTA_FISCAL: String,
      LAST_UPD: String,
    }
  }


  
</script>