<template>
    <div class="example-modal-content">
        <center>
            <h1><b>Peso</b></h1>
            <h1><b>{{ product[0].WEIGHT }}KG</b></h1>
            <br />
            <h2><b>Nota:{{ product[0].NOTA_FISCAL }}</b></h2>
            <br /> <br />
            <h3><b>{{ product[0].LAST_UPD }}</b></h3>
            <br />
   </center>
    </div>
</template>



<script>
    export default{
        data(){
            return{
                product:{}
            }
        },
        created: function(){
            this.getProduct();
        },
        methods: {
            getProduct: function()
            {
                this.$http.get('http://10.57.72.121:3012/searchid/' + this.$route.params.id).then((response) => {
                    this.product = response.data;
                }, (response) => {
                });
            },
 
        },

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
      font-size: 100px;
    }
    h2 {
      font-size: 90px;
    }
    h3 {
      font-size: 80px;
    }
</style>