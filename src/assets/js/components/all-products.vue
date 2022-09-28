<template>
    <div id="all-products">
        <center>
            <h1  class="text-primary">INVENTARIO - POS</h1>
        </center>
        <p><router-link :to="{ name: 'create_product' }" class="btn btn-primary">Cadastro Serial</router-link></p>
        <div class="form-group">
            <input type="text" name="search" v-model="productSearch" placeholder="Search Serial" class="form-control" v-on:keyup="searchProducts">
        </div>


            <!-- The Modal -->
            <div class="modal" id="myModal">
                <div class="modal-dialog">
                <div class="modal-content">
                
                    <div id="printMe" style="background:red;">
                        <p>葫芦娃，葫芦娃</p>
                        <p>一根藤上七朵花 </p>
                        <p>小小树藤是我家 啦啦啦啦 </p>
                        <p>叮当当咚咚当当　浇不大</p>
                        <p> 叮当当咚咚当当 是我家</p>
                        <p> 啦啦啦啦</p>
                        <p>...</p>
                    </div>

                 <button v-print="'#printMe'">Print local range</button>
                    
                    
                </div>
                </div>
            </div>

        <table class="table table-hover">
            <thead>
            <tr>
                <td>ID</td>
                <td>SERIAL</td>
                <td>NOTA_FISCAL</td>
                <td>LAST_UPD</td>
                <td>Actions</td>
            </tr>
            </thead>

            <tbody>
                
                <tr v-for="product in products">
                    <td>{{ product.ID }}</td>
                    <td>{{ product.SERIAL }}</td>
                    <td>{{ product.NOTA_FISCAL }}</td>
                    <td>{{ product.LAST_UPD }}</td>
                    <td>
                        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#myModal">
                            Print
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

    export default{
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
                    var productName = this.originalProducts[i]['SERIAL'].toLowerCase();
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
