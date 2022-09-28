<template>
    <div id="create-product">
        <center>
            <h1  class="text-primary">CADASTRO DE SERIAL</h1>
        </center>
        <p><router-link :to="{ name: 'all_products' }"  class="btn btn-primary">Voltar a Lista</router-link></p>
        <hr />
        <notification v-bind:notifications="notifications" class="alert alert-primary"></notification>
        <form v-on:submit.prevent="addProduct" id="form">
            <div class="form-group">
                <label name="product_price">NOTA_FISCAL</label>
                <input type="text" name="NOTA_FISCAL" ref="NOTA_FISCAL"  class="form-control" v-model="product.NOTA_FISCAL" maxlength="12" required> 
            </div>
            <div class="form-group">
                <label name="product_name">SERIAL</label>
                <input type="number" name="SERIAL" ref="SERIAL" class="form-control" 
                v-model="product.SERIAL"                  
                @input="updateValue" 
                autofocus maxlength="12" required /> 
            </div>
            <div class="form-group">
                <button class="btn btn-success">Create</button>
            </div>
        </form>
    </div>
</template>
<script>
import Notification from './notifications.vue';
    export default{
        data(){
            return{
                product:{},
                notifications:[],
                focused: false
            }
        },
        methods: {
             updateValue(event) {
                const value = event.target.value
                if (String(value).length <= 12) {
                    this.amount = value
                }
                this.$forceUpdate()
            },
           
            addProduct: function()
            {
                this.$http.post('http://10.57.65.125:3011/insertInvetarioPOS', this.product, {
                    headers : {
                        'Content-Type' : 'application/json'
                    }
                }).then((response) => {
                    this.notifications.pop();
                    this.notifications.push({
                        type: response.body.msg ?  'danger' : 'success',
                        message: response.body.msg ?  response.body.msg  : response.body.message
                    });
                    this.product.SERIAL = '';
                    this.$refs.SERIAL.focus()
                }, (response) => {
                    this.notifications.push({
                        type: 'error',
                        message: response.body.msg
                    });
                    this.product.SERIAL = '';       
                    this.$refs.SERIAL.focus()
                });
                this.focused = true;
            },
            onFocus() {
                this.focused = true
            },
            suggestTerms () {
                if ( this.product.SERIAL.length >= 12 ){
                    this.addProduct()
                }
            },
           
        },
        components: {
            'notification' : Notification
        }
    }
</script>
