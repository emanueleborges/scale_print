<template>
  <div class="example-modal-content">
   <center>
    <br />
    <h1><b>Peso</b></h1>
    <h1><b>{{ WEIGHT }}KG</b></h1>
    <br />
    <h2><b>Nota:{{ NOTA_FISCAL }}</b></h2>
    <br /> <br />
    <h3><b>{{ LAST_UPD }}</b></h3>
    <br />
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

<style scoped>
  /* ISO Paper Size */
  @page {
    size: A4 landscape;
  }
  
  /* Size in mm */    
  @page {
    size: 100mm 200mm landscape;
  }
  
  /* Size in inches */    
  @page {
    size: 4in 6in landscape;
  }
  h1 {
    font-size: 120px;
  }
  h2 {
    font-size: 110px;
  }
  h3 {
    font-size: 100px;
  }

    </style>
  
