<template>
  <v-container>
    <v-row>
      <v-col cols="2"></v-col>
      <v-col cols="8">
          <!-- <h1>{{indicator[0].Name}}</h1>
          <h4>{{indicator[0].description}}</h4>
          <h2>{{indicator[0].goal}}</h2>
          <h2>{{indicator[0].Tagline}}</h2>
          <h2>{{indicator[0].type}}</h2>
          <hr/>
          <h4>{{indicator[0].current_date}}</h4>
          <h2>{{indicator[0].current_value}}</h2>
          <h2>{{indicator[0].state_rank}}</h2>
          <h2>{{indicator[0].peer_rank}}</h2>
          <hr/>
          <h4>{{indicator[0].previous_date}}</h4>
          <h2>{{indicator[0].previous_value}}</h2>
          <h2>{{indicator[0].previous_state_rank}}</h2>
          <h2>{{indicator[0].previous_peer_rank}}</h2>
          <hr/>
          <h2>{{indicator[0].metric_trend}}</h2> -->

            <v-simple-table>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">
                      Name
                    </th>
                    <th class="text-left">
                      Value
                    </th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>Name</td>
                    <td>{{indicator[0].Name}}</td>
                  </tr>
                 <tr>
                    <td>
                      Description</td>
                    <td>{{indicator[0].description}}</td>
                  </tr>                 
                  <tr>
                    <td>Goal</td>
                    <td>{{indicator[0].goal}}</td>
                  </tr>
                  <tr>
                    <td>Tagline</td>
                    <td>{{indicator[0].Tagline}}</td>
                  </tr>
                 <tr>
                    <td>Type</td>
                    <td>{{indicator[0].type}}</td>
                  </tr>
                  <tr>
                    <td>Current Date</td>
                    <td>{{indicator[0].current_date}}</td>
                  </tr>
                  <tr>
                    <td>Current Value</td>
                    <td>{{indicator[0].current_value}}</td>
                  </tr>
                  <tr>
                    <td>State Rank</td>
                    <td>{{indicator[0].state_rank}}</td>
                  </tr>
                  <tr>
                    <td>Peer Rank</td>
                    <td>{{indicator[0].peer_rank}}</td>
                  </tr>
                  <tr>
                    <td>Previous Date</td>
                    <td>{{indicator[0].previous_date}}</td>
                  </tr>
                  <tr>
                    <td>Previous Value</td>
                    <td>{{indicator[0].previous_value}}</td>
                  </tr>
                  <tr>
                    <td>Previous State Rank</td>
                    <td>{{indicator[0].previous_state_rank}}</td>
                  </tr>
                  <tr>
                    <td> Previous Peer Rank</td>
                    <td>{{indicator[0].previous_peer_rank}}</td>
                  </tr>
                  <tr>
                    <td> Metric Trend</td>
                    <td>{{indicator[0].metric_trend}}</td>
                  </tr>
                  
                </tbody>
              </template>
            </v-simple-table>
  <hr/>

      </v-col>
         <v-col cols="2"></v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props:[
      'indicator'
    ],
    data: () => ({
      ecosystem: [
        {
          text: 'vuetify-loader',
          href: 'https://github.com/vuetifyjs/vuetify-loader',
        },
        {
          text: 'github',
          href: 'https://github.com/vuetifyjs/vuetify',
        },
        {
          text: 'awesome-vuetify',
          href: 'https://github.com/vuetifyjs/awesome-vuetify',
        },
      ],
      importantLinks: [
        {
          text: 'Documentation',
          href: 'https://vuetifyjs.com',
        },
        {
          text: 'Chat',
          href: 'https://community.vuetifyjs.com',
        },
        {
          text: 'Made with Vuetify',
          href: 'https://madewithvuejs.com/vuetify',
        },
        {
          text: 'Twitter',
          href: 'https://twitter.com/vuetifyjs',
        },
        {
          text: 'Articles',
          href: 'https://medium.com/vuetify',
        },
      ],
      whatsNext: [
        {
          text: 'Explore components',
          href: 'https://vuetifyjs.com/components/api-explorer',
        },
        {
          text: 'Select a layout',
          href: 'https://vuetifyjs.com/getting-started/pre-made-layouts',
        },
        {
          text: 'Frequently Asked Questions',
          href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
        },
      ],
    }),
  }
</script>
