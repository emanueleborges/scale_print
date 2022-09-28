<template>
    <div id="create-product" >
        <form v-on:submit.prevent="addProduct" id="form">
            <div class="form-group">
                <label name="product_peso">WEIGHT</label>
                <input type="text" name="WEIGHT" ref="WEIGHT" class="form-control" v-model="product.WEIGHT" autofocus maxlength="12" required /> 
            </div>
            <div class="form-group">
                <label name="product_price">NOTA FISCAL</label>
                <input type="text" name="NOTA_FISCAL" ref="NOTA_FISCAL"  class="form-control" v-model="product.NOTA_FISCAL"  maxlength="12" > 
            </div>
            <div class="form-group">
                <button class="btn btn-success">Salvar</button>
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
                this.$http.post('http://10.57.72.121:3012/insertprint', this.product, {
                    headers : {
                        'Content-Type' : 'application/json'
                    }
                }).then((response) => {
                    this.notifications.pop();
                    this.notifications.push({
                        type: response.body.msg ?  'danger' : 'success',
                        message: response.body.msg ?  response.body.msg  : response.body.message
                    });
                    this.product.WEIGHT = '';
                    this.$refs.WEIGHT.focus()
                }, (response) => {
                    this.notifications.push({
                        type: 'error',
                        message: response.body.msg
                    });
                    this.product.WEIGHT = '';       
                    this.$refs.WEIGHT.focus()
                });
                this.focused = true;
            },
            onFocus() {
                this.focused = true
            },
            suggestTerms () {
                if ( this.product.WEIGHT.length >= 12 ){
                    this.addProduct()
                }
            },
           
        },
        components: {
            'notification' : Notification
        }
    }
</script>
