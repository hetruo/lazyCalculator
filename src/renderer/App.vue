<template>
  <div id="app">
    <v-app light >
      <template>
        <div class="container">
          <v-flex xs12>
            <v-card>
              <v-layout row>
                <v-flex xs8>
                  <img src="./assets/resistor.svg" class="resistor">
                </v-flex>
                <v-flex xs4>
                  <v-text-field flat readonly solo v-model="value" class="resistance" style="margin-top: 80px; margin-left: -40px "></v-text-field>
                </v-flex>
              </v-layout>
              <v-container grid-list-sm>
                <template v-for="(color,i) in colors">
                  <v-layout row justify-space-around :key="'row'+i" style="margin-top:-10px">
                    <v-flex xs4>
                      <v-btn depressed small round :color=colors[i].rgb style="width:80%" @click="calculate(0,i)"></v-btn>
                    </v-flex>
                    <v-flex xs4>
                      <v-btn depressed small round :color=colors[i].rgb style="width:80%" @click="calculate(1,i)"></v-btn>
                    </v-flex>
                    <v-flex xs4>
                      <v-btn depressed small round :color=colors[i].rgb style="width:80%" @click="calculate(2,i)"></v-btn>
                    </v-flex>
                  </v-layout>
                </template>
              </v-container>
            </v-card>
          </v-flex>
        </div>

        <div class="container">
          <v-flex xs12>
            <v-card>
              <v-flex xs12>
                  <img src="./assets/capacitor.png" class="capacitor">
                </v-flex>
              <v-layout row justify-space-around>
                
                <v-flex xs3>
                  <v-text-field  v-model="capacitorIn" @keypress="calculateCapacitor('0')"></v-text-field>
                </v-flex>
                <v-flex xs3>
                  <v-select
                    label="Unidad"
                    :items="units"
                    @change="calculateCapacitor"
                  ></v-select>
                </v-flex>
                <v-flex xs3>
                  <v-text-field readonly v-model="capacitorOut"></v-text-field>
                </v-flex>
              </v-layout>
            </v-card>
          </v-flex>
        </div>

         
      </template>
    </v-app>
  </div>
</template>

<script>
  export default {
    name: 'lazyCalculator',
    data () {
      return {
        capacitorIn: '',
        capacitorOut: '',
        first: '',
        second: '',
        multiplier: '',
        value: '',
        colors: [
          {
            name: 'black',
            rgb: '#424242',
            value: '0',
            multiplier: 1
          },
          {
            name: 'brown',
            rgb: '#5D4037',
            value: '1',
            multiplier: 10
          },
          {
            name: 'red',
            rgb: '#FF5252',
            value: '2',
            multiplier: 100
          },
          {
            name: 'orange',
            rgb: '#F57C00',
            value: '3',
            multiplier: 1000
          },
          {
            name: 'yellow',
            rgb: '#FFEE58',
            value: '4',
            multiplier: 10000
          },
          {
            name: 'green',
            rgb: '#689F38',
            value: '5',
            multiplier: 100000
          },
          {
            name: 'blue',
            rgb: '#0091EA',
            value: '6',
            multiplier: 1000000
          },
          {
            name: 'purple',
            rgb: '#D500F9',
            value: '7',
            multiplier: 10000000
          },
          {
            name: 'grey',
            rgb: '#90A4AE',
            value: '8',
            multiplier: 100000000
          },
          {
            name: 'white',
            rgb: '#ECEFF1',
            value: '9',
            multiplier: 1000000000
          }
        ],
        units: ['Nano','Mili'],
        unit: ''
      }
    },
    methods: {
      calculate (column,row) {
        if(column===0){
          this.first = this.colors[row].value
        }
        if(column===1) {
          this.second = this.colors[row].value
        }
        if(column===2) {
          this.multiplier = this.colors[row].multiplier
        }
        if(this.first!==''&&this.second!==''&&this.multiplier!==''){
          var r = parseInt(this.first+this.second)*this.multiplier
          if(r>=1000 && r <1000000) {
            r = r/1000 + ' K'
          }
          else if (r>=1000000){
            r = r/1000000 + ' M'
          }
          this.value = r+' Ω'
        }
      },
      calculateCapacitor (input) {
        if(!Number.isInteger(input)){
          this.unit = input
        }
        if(this.unit!==undefined && this.capacitorIn!==''){
          if(this.unit==='Mili') {
              this.capacitorOut = this.capacitorIn*1000+' Micros'
          }
          else {
            this.capacitorOut = this.capacitorIn/1000+' Micros'
          }
        }
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons');
  
  .resistor{
    padding-top:20px;
    padding-bottom: 20px;
    display: block;
    margin-left: 60px;
    width: 70%
  }
  .resistance {
    font-size:38px; 
  }
  .capacitor {
    padding-top:30px;
    margin-left: 400px;
    padding-bottom: 20px;
    width: 60px;
  }

</style>
