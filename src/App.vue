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
                  Education
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
                  Justice
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
                  Government
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
    </v-navigation-drawer>

    <v-content app>
      <v-container fluid>

        <v-row id="firstRow">
              <h2>Texas 2036 Indicators Update</h2>
              <hr/>
        </v-row>
        <v-row class="fill-height">
            <v-col>

              <!-- <div id="holder"></div> -->
               <v-data-table
               v-if="showTable"
                dense
                :headers="headers"
                :items="filteredIndicators"
                item-key="name"
                class="elevation-1"
                items-per-page="50"
              ></v-data-table>
              <div id="markdown" v-if="!showTable">
                  <hello-world v-bind:indicator="selectedIndicator"></hello-world>
                
              </div>
            </v-col>
        </v-row>
      </v-container>
    </v-content>



  </v-app>
</template>

<script>
import inds from './assets/indicators.json';
import _ from 'lodash';
import { marked } from 'marked';
import JQuery from 'jquery';
import HelloWorld from './components/HelloWorld.vue';
const $ = JQuery;

export default {
  components: { HelloWorld },
  name: 'App',
  data: () => ({
    showTable:true,
    drawer: true,
    indicators:inds,
    filteredIndicators:[],
    selectedIndicator:{},
    areas:["Education", "Prosperity", "Justice", "Health", "Infrastructure", "Natural Resources", "Government"],
    headers: [
        {
          text: 'Name',
          align: 'start',
          sortable: false,
          value: 'Name',
        },
        { text: 'Tagline', value: 'Tagline' },
        { text: 'Goal', value: 'goal' },
        { text: 'Policy Area', value: 'policy_area' },
        { text: 'Type', value: 'type' },
        { text: 'Current Value', value: 'current_value' }
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
    this.filteredIndicators=inds;
  },
  mounted(){
    this.loader();
  },
  methods:{
      loadTable(area){
        this.showTable=true;
        this.filteredIndicators = _.filter(inds, {
          "policy_area":area
        });
    },
    loadIndicator(ind_name){
          this.showTable=false;
          this.selectedIndicator = _.filter(inds, {
            "Name":ind_name
        });
        console.log(ind_name);
        console.log(this.selectedIndicator[0].Tagline);




    },
    loader(){
        $.get('https://mapfiles.blob.core.windows.net/misc/report.md', function(data) {
              console.log("report data");
              console.log(data);
              $("#holder").html(marked.parse(data));
        });
        //       $.get('../assets/report.md', function(data) {
        //       console.log("report data");
        //       console.log(data);
        //       $("#holder").html(marked.parse(data));
        // });
    }
  }
};
</script>
<style scoped>
#firstRow{
  justify-content: center;
  margin-top:8px !important;
}
.v-data-table{
  margin-top:15px !important;
}
.v-navigation-drawer{
  width:350px !important;
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
  margin-left:100px;
}
</style>
