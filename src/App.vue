<template>
  <v-app>
   <v-app-bar app clipped-left>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Texas 2036</v-toolbar-title>
        <v-spacer></v-spacer>
                <v-btn href="https://github.com/robertmundinger/Texas_Indicators" target="_blank" text>
            <span class="mr-2">Github</span>
            <v-icon>mdi-open-in-new</v-icon>
        </v-btn>
    </v-app-bar>

    <v-navigation-drawer app clipped left v-model="drawer">
          <v-card
          class="mx-auto"
          max-width="400"
          min-width="350"
          app
          flat
        >
            <v-expansion-panels flat>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`education`)">
                  Education & Workforce
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in education" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`prosperity`)">
                  Prosperity
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in prosperity" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`health`)">
                  Health
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in health" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`justice`)">
                  Justice & Safety
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in justice" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`infrastructure`)">
                  Infrastructure
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in infrastructure" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

                            <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`natural resources`)">
                  Natural Resources
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in naturalresources" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>

              <v-expansion-panel>
                <v-expansion-panel-header @click="loadTable(`government`)">
                  Government Performance
                </v-expansion-panel-header>
                <v-expansion-panel-content>
                    <v-list-item v-for="h in government" :key="h.Name" @click="loadIndicator(h.Name)">
                      <v-list-item-content>
                        <v-list-item-subtitle>{{h.Name}}</v-list-item-subtitle>
                      </v-list-item-content>
                    </v-list-item>
                </v-expansion-panel-content>
              </v-expansion-panel>




            </v-expansion-panels>
        </v-card>

        <v-btn @click="loadChart()">Show Stacked Chart</v-btn>
    </v-navigation-drawer>

    <v-content app>
      <v-container fluid>

        <v-row id="firstRow">
          <v-col cols="12">
              <h2>Texas 2036 Indicators Update</h2>
              <hr/>
          </v-col>
        </v-row>

      <v-row>
        <!-- <v-cols cols="2">
          <v-combobox
              v-model="select"
              :items="combos"
              label="Type"
              outlined
              dense
              solo
              style="margin-left:12px;"
              @change="changeType"
            ></v-combobox>
        </v-cols> -->
       <v-cols cols="2">
          <v-combobox
              v-model="select2"
              :items="trends"
              label="Trend"
              outlined
              dense
              solo
              style="margin-left:12px;"
              @change="changeTrend"
            ></v-combobox>
        </v-cols> 
        <v-cols cols="2">
          <v-combobox
              v-model="select3"
              :items="area_keys"
              label="Policy Area"
              outlined
              solo
              dense
              style="margin-left:12px;"
              @change="changeArea"
            ></v-combobox>
        </v-cols>
                <v-cols cols="2">
          <v-btn
            style="margin-left:12px; height:40px;"
              @click="clearFilters"
            >Clear Filters</v-btn>
        </v-cols>
        </v-row>

        <v-row class="fill-height">
            <v-col cols="12">
              
               <v-data-table
               v-if="showTable"
                dense
                light
                fixed-header
                :headers="headers"
                :items="filteredIndicators"
                item-key="name"
                class="table-striped elevation-1"
                items-per-page="62"
                height="65vh"
              >
              <!-- <template v-slot:[`filteredIndicators.trend`]="{filteredIndicators}">
                <div :class="getStyle(filteredIndicators.trend)">{{ filteredIndicators.trend }}</div>
              </template> -->
              </v-data-table>
            
              <div id="markdown" v-if="showDetail">
                  <hello-world v-bind:indicator="selectedIndicator"></hello-world>
                
              </div>

               <div id="charter" v-if="showChart">
                  <Stacked></Stacked>
                
              </div>
            </v-col>
        </v-row>
      </v-container>
    </v-content>



  </v-app>
</template>

<script>
import inds from './assets/indicators_2.json';
import _ from 'lodash';
import { marked } from 'marked';
import HelloWorld from './components/HelloWorld.vue';
//import JQuery from 'jquery';
//const $ = JQuery;
import Stacked from "./components/Stacked";

export default {
  components: { HelloWorld, Stacked },
  name: 'App',
  data: () => ({
    combos:["Primary", "Secondary"],
    trends:["Up", "Down", "Flat"],
    showTable:true,
    showChart:false,
    showDetail:false,
    drawer: true,
    indicators:inds,
    isFiltered:false,
    filteredIndicators:[],
    primaryIndicators:[],
    selectedIndicator:{},
    areas:["Education & Workforce", "Prosperity", "Justice & Safety", "Health", "Infrastructure", "Natural Resources", "Government"],
    area_keys:[
      {
       name:"education",
       title:"Education & Workforce"
      },
      {
       name:"prosperity",
       title:"Prosperity"
      },
           {
       name:"justice",
       title:"Justice & Safety"
      },
            {
       name:"health",
       title:"Health"
      },
            {
       name:"infrastructure",
       title:"Infrastructure"
      },
            {
       name:"natural resources",
       title:"Natural Resources"
      },
            {
       name:"government",
       title:"Government Performance"
      }
    ],
    headers: [
        { text: 'Goal #', value: 'goal_number' },
        { text: 'Goal', value: 'goal' },
        {
          text: 'Name',
          align: 'start',
          sortable: false,
          value: 'Name',
        },
        // { text: 'Tagline', value: 'Tagline' },
        { text: 'Policy Area', value: 'policy_area' },
        { text: 'Type', value: 'type' },
        { text: 'Current Date', value: 'current_date' },
        { text: 'Current Value', value: 'current_value' },
        { text: 'State Rank', value: 'state_rank' },
        { text: 'Peer Rank', value: 'peer_rank' },

        { text: 'Previous Date', value: 'previous_date' },
        { text: 'Previous Value', value: 'previous_value' },
        { text: 'Previous State Rank', value: 'previous_state_rank' },
        { text: 'Previous Peer Rank', value: 'previous_peer_rank' },
        { text: 'Trend', value: 'metric_trend' }
      ],
  }),
  computed:{
        my_marked:function(){
        return  marked.parse('# Marked in Node.js\n\nRendered by **marked**.');
    },
    health: function(){
      return  _.filter(inds, {"policy_area":"health", "type":"Primary"});
    },
    justice: function(){
      return  _.filter(inds, {"policy_area":"justice", "type":"Primary"});
    },
    education: function(){
      return  _.filter(inds, {"policy_area":"education", "type":"Primary"});
    },
    prosperity: function(){
      return  _.filter(inds, {"policy_area":"prosperity", "type":"Primary"});
    },
    infrastructure: function(){
      return  _.filter(inds, {"policy_area":"infrastructure", "type":"Primary"});
    },
    naturalresources: function(){
      return  _.filter(inds, {"policy_area":"natural resources", "type":"Primary"});
    },
    government: function(){
      return  _.filter(inds, {"policy_area":"government", "type":"Primary" });
    }
  },
  created(){
    //this.filteredIndicators=inds;
    this.filteredIndicators = _.filter(inds, {
          "type":"Primary"
        });

    this.primaryIndicators = _.filter(inds, {
            "type":"Primary"
          });
    this.filteredIndicators= _.orderBy(this.filteredIndicators, ['goal_number'],['asc']);
    //this.primaryIndicators= _.orderBy(this.primaryIndicators, ['goal_number'],['asc']);
  },
  mounted(){
    //this.loader();
  },
  methods:{
    clearFilters(){
      this.filteredIndicators=inds;
      this.filteredIndicators = _.filter(inds, {
            "type":"Primary"
          });



      this.isFiltered=false;
    },
    changeType(value){
      if(this.isFiltered){
          this.filteredIndicators = _.filter(this.filteredIndicators, {
            "type":value
          });
      }
      else{
        this.filteredIndicators = _.filter(inds, {
            "type":value
          });
      }

    },
    changeTrend(value){

      if(this.isFiltered){
        this.filteredIndicators = _.filter(this.filteredIndicators, {
          "metric_trend":value
        });
      }
      else{
        this.filteredIndicators = _.filter(this.primaryIndicators, {
            "metric_trend":value
          });
      }
      this.isFiltered=true;
    },
    changeArea(value){

      if(this.isFiltered){
        this.filteredIndicators = _.filter(this.filteredIndicators, {
          "policy_area":value
        });
      }
      else{
        this.filteredIndicators = _.filter(this.primaryIndicators, {
            "policy_area":value
          });
      }

      this.isFiltered=true;
    },



    loadTable(area){
        this.showTable=true;
        this.showDetail=false;
        this.showChart=false;
         this.filteredIndicators= _.filter(inds, {
          "policy_area":area, "type":"Primary"
        });
//        this.filteredIndicators= _.orderBy(this.filteredIndicators, ['goal_number'],['asc']);
    },
    loadIndicator(ind_name){
          this.showTable=false;
          this.showChart=false;
          this.showDetail=true;
          this.selectedIndicator = _.filter(inds, {
            "Name":ind_name
        });
        //console.log(ind_name);
        //console.log(this.selectedIndicator[0].Tagline);




    },

    getStyle (trend) {
      console.log("trend");
      console.log(trend);
      if (trend == "Up") return 'red--text font-weight-bold'
      else return ''
    },
    loadChart(){
      this.showTable=false;
      this.showDetail=false;
      this.showChart=true;

    }
    //     loader(){
    //     $.get('https://mapfiles.blob.core.windows.net/misc/report.md', function(data) {
    //           //console.log("report data");
    //           //console.log(data);
    //           $("#holder").html(marked.parse(data));
    //     });
    //     //       $.get('../assets/report.md', function(data) {
    //     //       console.log("report data");
    //     //       console.log(data);
    //     //       $("#holder").html(marked.parse(data));
    //     // });
    // }
  }
};
</script>
<style>
#firstRow{
  justify-content: center;
  margin-top:8px !important;
}
.v-data-table{
  margin-top:15px !important;
}
.v-navigation-drawer{
  width:225px !important;
}
.v-list-item__subtitle{
  padding:2px !important;
}
.v-list-item__content{
  padding:0px !important;
}
.v-list-item {
  padding:0px !important;
  height:30px !important;
  min-height:30px !important;
}
main{
  background-color: #3a4a9f;
  margin-left:0px;
  
}
.v-main__content{
  overflow-x: scroll;
}
fieldset{
  background-color: white;
}
thead.v-data-table-header{
  height:75px !important;
}
  tbody tr:nth-of-type(even) {
    background-color: rgba(236, 237, 237);
  }

  tbody tr:nth-of-type(odd) {
    background-color: rgb(250 ,250, 250);
  }

  .v-data-table-header {
    background-color: rgba(182, 183, 187);
    color: white;
  }

  .v-data-footer {
    background-color: rgb(250 ,250, 250);
  }

.layout {
  display: inline-block;
  width: 100%;
}

</style>
