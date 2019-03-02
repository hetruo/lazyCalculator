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

                <template v-for="(band,i) in band1">
                  <v-layout row justify-space-around :key="'row'+i" style="margin-top:-5px">
                    <v-flex xs4>
                      <v-btn  small  :color=band1[i].rgb style="width:80%" @click="calculate(1,i)" :round=band1[i].selected ></v-btn>
                    </v-flex>
                    <v-flex xs4>
                      <v-btn  small  :color=band2[i].rgb style="width:80%" @click="calculate(2,i)" :round=band2[i].selected ></v-btn>
                    </v-flex>
                    <v-flex xs4>
                      <v-btn  small  :color=band3[i].rgb style="width:80%" @click="calculate(3,i)" :round=band3[i].selected ></v-btn>
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
        band1: [
          {
            name: 'black',
            rgb: '#424242',
            value: '0',
            selected: false
          },
          {
            name: 'brown',
            rgb: '#5D4037',
            value: '1',
            selected: false
          },
          {
            name: 'red',
            rgb: '#FF5252',
            value: '2',
            selected: false
          },
          {
            name: 'orange',
            rgb: '#F57C00',
            value: '3',
            selected: false
          },
          {
            name: 'yellow',
            rgb: '#FFEE58',
            value: '4',
            selected: false
          },
          {
            name: 'green',
            rgb: '#689F38',
            value: '5',
            selected: false
          },
          {
            name: 'blue',
            rgb: '#0091EA',
            value: '6',
            selected: false
          },
          {
            name: 'purple',
            rgb: '#D500F9',
            value: '7',
            selected: false
          },
          {
            name: 'grey',
            rgb: '#90A4AE',
            value: '8',
            selected: false
          },
          {
            name: 'white',
            rgb: '#ECEFF1',
            value: '9',
            selected: false
          }
        ],
        band2: [
          {
            name: 'black',
            rgb: '#424242',
            value: '0',
            selected: false
          },
          {
            name: 'brown',
            rgb: '#5D4037',
            value: '1',
            selected: false
          },
          {
            name: 'red',
            rgb: '#FF5252',
            value: '2',
            selected: false
          },
          {
            name: 'orange',
            rgb: '#F57C00',
            value: '3',
            selected: false
          },
          {
            name: 'yellow',
            rgb: '#FFEE58',
            value: '4',
            selected: false
          },
          {
            name: 'green',
            rgb: '#689F38',
            value: '5',
            selected: false
          },
          {
            name: 'blue',
            rgb: '#0091EA',
            value: '6',
            selected: false
          },
          {
            name: 'purple',
            rgb: '#D500F9',
            value: '7',
            selected: false
          },
          {
            name: 'grey',
            rgb: '#90A4AE',
            value: '8',
            selected: false
          },
          {
            name: 'white',
            rgb: '#ECEFF1',
            value: '9',
            selected: false
          }
        ],
        band3: [
          {
            name: 'black',
            rgb: '#424242',
            multiplier: 1,
            selected: false
          },
          {
            name: 'brown',
            rgb: '#5D4037',
            multiplier: 10,
            selected: false
          },
          {
            name: 'red',
            rgb: '#FF5252',
            multiplier: 100,
            selected: false
          },
          {
            name: 'orange',
            rgb: '#F57C00',
            multiplier: 1000,
            selected: false
          },
          {
            name: 'yellow',
            rgb: '#FFEE58',
            multiplier: 10000,
            selected: false
          },
          {
            name: 'green',
            rgb: '#689F38',
            multiplier: 100000,
            selected: false
          },
          {
            name: 'blue',
            rgb: '#0091EA',
            multiplier: 1000000,
            selected: false
          },
          {
            name: 'purple',
            rgb: '#D500F9',
            multiplier: 10000000,
            selected: false
          },
          {
            name: 'grey',
            rgb: '#90A4AE',
            multiplier: 100000000,
            selected: false
          },
          {
            name: 'white',
            rgb: '#ECEFF1',
            multiplier: 1000000000,
            selected: false
          }
        ],
        units: ['Nano','Mili'],
        selectedUnit: ''
      }
    },
    methods: {
      calculate (band,color) {
        var i  
        if(band===1){
          for(i=0; i<this.band1.length; i++){
            this.band1[i].selected = false
          }
          this.first = this.band1[color].value
          this.band1[color].selected = true
        }
        if(band===2) {
          for(i=0; i<this.band2.length; i++){
            this.band2[i].selected = false
          }
          this.second = this.band2[color].value
          this.band2[color].selected = true
        }
        if(band===3) {
          for(i=0; i<this.band3.length; i++){
            this.band3[i].selected = false
          }
          this.multiplier = this.band3[color].multiplier
          this.band3[color].selected = true
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
          this.selectedUnit = input
        }
        if(this.selectedUnit!==undefined && this.capacitorIn!==''){
          if(this.selectedUnit==='Mili') {
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
