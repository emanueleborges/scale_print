<template>
    <div id="all-products">
        <center>
            <h1  class="text-primary">SCALE PRINTER</h1>
        </center>
        <Create/>
        <div class="form-group">
            <input type="text" name="search" v-model="productSearch" placeholder="Search Serial" class="form-control" v-on:keyup="searchProducts">
        </div>
   
        <table class="table table-hover">
            <thead>
            <tr>
                <td>ID</td>
                <td>WEIGHT</td>
                <td>NOTA_FISCAL</td>
                <td>LAST_UPD</td>
                <td>Actions</td>
            </tr>
            </thead>

            <tbody>              
                <tr v-for="product in products">
                    <td>{{ product.ID }}</td>
                    <td>{{ product.WEIGHT }}</td>
                    <td>{{ product.NOTA_FISCAL }}</td>
                    <td>{{ product.LAST_UPD }}</td>
                    <td>
                        <button type="button" class="btn btn-primary" data-toggle="modal" v-bind:data-target="'#myModal-'+product.ID">
                            Print
                        </button>
                    </td>

                    <div class="modal" v-bind:id="'myModal-'+product.ID">
                        <div class="modal-dialog">
                            <div class="modal-content">
                                <div id="printMe">
                                    <Detalhes :WEIGHT="product.WEIGHT" :NOTA_FISCAL="product.NOTA_FISCAL" :LAST_UPD="product.LAST_UPD"></Detalhes>
                                </div>
                            <button v-print="'#printMe'">Print Label</button>  
                            </div>
                        </div>
                    </div>

                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

    import Create from "./create-product.vue";
    import Detalhes from "./modal/Detalhes.vue";

    export default{

        components: {
            Create,
            Detalhes
        },

        data(){
            return{
                products: [],
                originalProducts: [],
                productSearch: ''
            }
        },

        created: function()
        {
            this.fetchProductData();
        },

        methods: {
            fetchProductData: function()
            {
                this.$http.get('http://10.57.72.121:3012/testprint').then((response) => {
                    this.products = response.body;
                    this.originalProducts = this.products;
                }, (response) => {

                });
            },

            searchProducts: function()
            {
                if(this.productSearch == '')
                {
                    this.products = this.originalProducts;
                    return;
                }

                var searchedProducts = [];
                for(var i = 0; i < this.originalProducts.length; i++)
                {
                    var productName = this.originalProducts[i]['ID'].toLowerCase();
                    if(productName.indexOf(this.productSearch.toLowerCase()) >= 0)
                    {
                        searchedProducts.push(this.originalProducts[i]);
                    }
                }

                this.products = searchedProducts;
            }
        }
    }
</script>
