<template>
    <div class="conversor">
        <h2 class="coin-header">{{ moedaA }} To {{ moedaB }}</h2>
        <input class="input-field" type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input class="submit" type="button" value="Converter" v-on:click="converter">
        <h2>{{ moedaB_value }}</h2>
    </div>
</template>

<script>
/* eslint-disable */
export default {
    name: "Conversor",
    props: ["moedaA", "moedaB"],
    data() {
        return {
            moedaA_value: "",
            moedaB_value: 0
        }
    },
    methods:{
        converter(){
            let from_to = this.moedaA + "_" + this.moedaB;

            let url = "https://free.currencyconverterapi.com/api/v5/convert?q="+ from_to +"&compact=y";

            fetch(url).then(res=>{
                return res.json();
            }).then(json=>{
                let cotacao = json[from_to].val;
                this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
            })
        }
    }
};
</script>

<style scoped>
    .conversor{
        padding: 20px;
        max-width: 300px;
        border-radius: 8px;
        background-color: rgb(255, 220, 122);
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
    }
    .coin-header{
        text-align: center;
        margin-top: 5px;
    }
    .input-field{
        border-style: double;
        border-color: rgb(134, 134, 134);
        border-radius: 4px;
        margin-right: 8px;
        height: 20px;
    }
    .submit{
        background-color: black;
        color: white;
        border-color: black;
        border-radius: 4px;
        height: 26px;
    }
</style>
