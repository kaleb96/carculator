<script setup>
import {ref, watch, reactive} from 'vue';

const state = reactive({
    result : '',
    operation : ''
})

const tmpValue1 = ref('');
const tmpValue2 = ref('');

watch(() => state.result, (newValue, oldValue) => {

    if(state.operation != '') {
        console.log('stateOperation : ' + state.operation);
    }
    // console.log('newValue = ' + newValue);
    // console.log('oldValue = ' + oldValue);

});

const clickInput = (e) => {
    
    let isOperation = checkOperation(e);

    if(e === 'c') { // Clear All
        state.result = '';

    } else if(e === 'd') { // Delete
        if(state.result.length > 0) {
            state.result = state.result.substring(0, (len.value-1));
        } else {
            state.result = '';
        }

    } else if(e === '=') { // Carculate

    } else if(isOperation) {

        useOperation(e);
    } else {
        state.result += e;
    }
}

const checkOperation = (e) =>{
    
    if(e === '+' || e === 'x' || e === '-' || e ==='/') {
        return true;
    } else {
        return false;
    }
}

const useOperation = (e) => {

    if(state.result.length > 0) {

        state.operation = e;
       
        if(!checkOperation(state.result[state.result.length - 1])) { // 마지막 문자가 연산기호가 아닌경우 
            state.result += state.operation;

        } else { // 마지막 문자가 연산기호인 경우
            // console.log('마지막 문자가 연산기호임');
            let strArray = state.result.split('');

            // 배열의 마지막 요소를 변경
            strArray[strArray.length - 1] = e;
 
            // 변경된 배열을 다시 문자열로 변환
            state.result = strArray.join('');
            // console.log('stateResult = ' + state.result);
        }
           
    }
  
}
</script>

<template>
    
    <div class="car-container">
        <v-col
        cols="12"
        sm="4"
        >
        <p>Carculator</p>

            <v-btn-toggle >
                <v-btn min-width="96px" > </v-btn>
                <v-btn @click="clickInput('c')">C</v-btn>
                <v-btn @click="clickInput('d')"><-</v-btn>
            </v-btn-toggle>

            <v-btn-toggle >
                <v-btn @click="clickInput('7')">7</v-btn>
                <v-btn @click="clickInput('8')">8</v-btn>
                <v-btn @click="clickInput('9')">9</v-btn>
                <v-btn @click="clickInput('/')">/</v-btn>
            </v-btn-toggle>

            <v-btn-toggle>
                <v-btn @click="clickInput('4')">4</v-btn>
                <v-btn @click="clickInput('5')">5</v-btn>
                <v-btn @click="clickInput('6')">6</v-btn>
                <v-btn @click="clickInput('x')">x</v-btn>
            </v-btn-toggle>

            <v-btn-toggle >
                <v-btn @click="clickInput('1')">1</v-btn>
                <v-btn @click="clickInput('2')">2</v-btn>
                <v-btn @click="clickInput('3')">3</v-btn>
                <v-btn @click="clickInput('-')">-</v-btn>
            </v-btn-toggle>

            <v-btn-toggle >
                <v-btn @click="clickInput('.')">.</v-btn>
                <v-btn @click="clickInput('3')">0</v-btn>
                <v-btn @click="clickInput('=')">=</v-btn>
                <v-btn @click="clickInput('+')">+</v-btn>
            </v-btn-toggle>
        </v-col>
        <div>{{ state.result }}</div>
    </div>
</template>

<style scoped>
.car-container{
    padding: 0;
    margin: 0;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
