<template>
  <div>
    <h1 class="blue--text title">My Projects</h1>
   <v-expansion-panels focusable>
      <v-expansion-panel
          v-for="project in projects" :key="project.project"
      >
        <v-expansion-panel-header class="purple--text title">{{ project.project }}</v-expansion-panel-header>
        <v-expansion-panel-content class="red--text title">
         {{ project.content }}
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
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
  computed: {
    myProjects() {
      return this.projects.filter(project => {
        return project.person === 'The Net Ninja' && project.status != 'complete'
      })
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
