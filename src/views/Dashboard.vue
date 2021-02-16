<template>
  <div>
    <h1 class="subheading blue--text">Dashboard</h1>
    <v-container class="my-5">

      <v-layout row justify-start class="mb-3">
        <v-tooltip top>
          <v-btn small flat color="grey" @click="sortBy('title')" slot="activator">
            <v-icon small left>folder</v-icon>
            <span class="caption text-lowercase">By project name</span>
          </v-btn>
          <span>Sort by project name</span>
        </v-tooltip>
        <v-tooltip top>
          <v-btn small flat color="grey" @click="sortBy('person')" slot="activator">
            <v-icon small left>person</v-icon>
            <span class="caption text-lowercase">By Person</span>
          </v-btn>
          <span>Sort by project author</span>
        </v-tooltip>
      </v-layout>

      <v-card  class="pa-3 blue--text" v-for="project in projects" :key="project.title">
      <v-layout row wrap :class="`pa-3 project ${project.status}`">
        <v-flex xs12 md6>
          <div class="caption blue--text">Project title</div>
          <div>{{ project.title }}</div>
        </v-flex>
        <v-flex xs6 sm4 md2>
          <div class="caption blue--text">Person</div>
          <div>{{ project.person }}</div>
        </v-flex>
        <v-flex xs6 sm4 md2>
          <div class="caption blue--text">Deadline</div>
          <div>{{ project.deadline }}</div>
        </v-flex>
        <v-flex xs2 sm4 md2>
          <div class="caption blue--text">Status</div>
          <div>{{ project.status }}
          </div>
        </v-flex>
      </v-layout>
      </v-card>
    </v-container>

  </div>
</template>

<script>
import db from '@/fb'
export default {
  data() {
    return {
      projects: []
    }
  },
  methods: {
    sortBy(prop) {
      this.projects.sort((a,b) => a[prop] < b[prop] ? -1 : 1)
    }
  },
  created() {
    db.collection('projects').onSnapshot(res => {
      const changes = res.docChanges();
      changes.forEach(change => {
        if (change.type === 'added') {
          this.projects.push({
            ...change.doc.data(),
            id: change.doc.id
          })
        }
      })
    })
  }
}
</script>

<style>

.project.complete {
  border-bottom: 5px solid purple;
  background: purple;
}
.project.ongoing {
  border-bottom: 5px solid yellow;
  background: yellow;
}
.project.overdue {
  border-bottom: 5px solid red;
  background: red;
}

</style>