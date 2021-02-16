<template>
  <div class="team">
    <h1 class="subheading blue--text">Team</h1>

    <v-container class="my-5">


      <v-layout row wrap>
        <v-flex xs12 sm6 md 4 lg3 v-for="person in team" :key="person.name">
          <v-card class="text-center ma-3">
            <v-responsive class="pt-4">
               <v-avatar size="100">
                 <img :src="person.avatar">
               </v-avatar>
            </v-responsive>
             <v-card-text>
               <div class="blue--text title font-weight-bold">{{ person.name }}</div>
               <div class="blue--text">{{ person.role }}</div>
             </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>


    </v-container>

  </div>
</template>

<script>
export default {
 data() {
   return {
     team: [
       { name: 'Iulian', role:'Web developer', avatar: '/iul.png'},
       { name: 'Darius', role:'Math teacher', avatar: '/dar.png'},
       { name: 'Razvan', role:'History teacher', avatar: '/raz.png'},
     ]
   }
 }
}
</script>
