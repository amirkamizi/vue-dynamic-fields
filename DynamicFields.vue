<template>
    <div class="card">
        <div class="card-header">
            Dynamic Form and Inputs
        </div>
        <div class="card-body">
            <p>Total Remainder: {{totalAmount}}</p>
            <form v-on:sumbit.prevent>
            <div class="form-inline border p-2" v-for="f in fromField" v-bind:key="f.id">
                <label>Name</label>
                <input class="form-control m-1" type="text" v-model="f.name">
                <label>Currency</label>
                <input class="form-control m-1" type="text" v-model="f.currency">
                <label>Total</label>
                <input class="form-control m-1" type="text" v-model.number="f.total">
                <button class="btn btn-danger btn-sm" v-on:click="removeField(f.id)">X</button>
            </div>
            </form>
            <div class="form-inline my-2">
                <label>Account</label>
                <select class="form-control m-1" v-model="newName">
                    <option v-for="account in accounts" :key="account.id">{{ account }}</option>
                </select>
                <label>Currency</label>
                <select class="form-control m-1" v-model="newcurrency">
                    <option v-for="cur in currencies" :key="cur.id">{{ cur }}</option>
                </select>
                <!-- <input type="text" v-model="newcurrency"> -->
                <label>Amount</label>
                <input class="form-control m-1" type="text" v-model.number="newTotal">
                <button class="btn btn-info" v-on:click="addNew">ADD</button>
            </div>
            <br>
            <button class="btn btn-success" v-on:click="submitForm">Submit Accounting</button>
            <br>
            <p class="my-2">{{finalAccounting}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                finalAccounting:'',
                accounts :['Shopping','John','Salary','Rent','Other'],
                currencies :['EUR','USD','TRY','RIAL'],
                newName : 'Shopping',
                newcurrency: 'EUR',
                newTotal: 0,
                fromField :[
                ]
            }
        },
        computed:{
            totalAmount:function(){
                var temp = 0;
                for (let index = 0; index < this.fromField.length; index++) {
                    temp+= this.fromField[index].total;
                }
                return temp;
            }
        },
        methods:{
            addNew : function(){
                this.fromField.push({
                    name: this.newName,
                    currency : this.newcurrency,
                    total : this.newTotal
                });
                this.resetNew();
            },
            removeField: function(id){
                this.fromField.splice(id,1);
            },
            resetNew : function(){
                this.newName = '';
                this.newcurrency = '';
                this.newTotal= 0;
            },
            submitForm : function(){
                this.finalAccounting = JSON.stringify(this.fromField);
                for (let index = 0; index < this.fromField.length; index++) {
                   console.log(JSON.stringify(this.fromField[index]));
                }
            }
        }
    }
</script>
