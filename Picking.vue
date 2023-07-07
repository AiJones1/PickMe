<template>
    <body>
        
        <v-btn @click="toggleView()">Toggle View</v-btn>


    <div id ="randomArray">
        <h1>Picking<v-select label="Select" 
            :items="['Dinner', 'Date']"
            variant="solo-filled"
            ></v-select></h1>


                <v-btn @click="pickDinner()">Choose Now</v-btn>

        <h3>Tonight's pick: {{ tonightDinner }}</h3>





    </div>

    <div id ="myDiv">
        <h1>This is toggling display</h1>

        <v-text-field
        @keydown.enter="addDinner(input)"
        label="add your own favourite options!"
        v-model="input"
    ></v-text-field>
                <v-btn @click="addDinner(input)">Add your favourite meals</v-btn>

    </div>

    </body>
   
</template>
<script setup>
import { ref,  computed } from 'vue'
import { set } from '@vueuse/core'

// reactive state
const input = ref('')
const dinner = ['chicken', 'death', 'kebabs']
const date = ['movie', 'restaurant', 'arcade']
var tonightDinner = ref(' ')


function pickDinner() {
    tonightDinner.value = dinner[Math.floor(Math.random() * dinner.length)]
    console.log(dinner.length)
    console.log(tonightDinner.value)
}

// function pickChosenCategory(selection){
//     tonightChoice.value = selection[Math.floor(Math.random()*selection.length)]
// }

function addDinner(din) {
    dinner.push(din)
    set(input, '')
}

function toggleView(){
    var x = document.getElementById("myDiv")
    var y= document.getElementById("randomArray")
    if(x.style.display=="none"){
        x.style.display = "block"
        y.style.display ="none"
    } else {
        x.style.display = "none"
        y.style.display = "block"
    }
}

// lifecycle hooks
</script>
<style></style>
