<template>
  <div class="row">
    <div class="col s12 m7">
      <CardProject v-for="(project, i) in projects" :key="i" :data="project" />
    </div>
  </div>
</template>

<script>
import CardProject from "../components/CardProject.vue";

export default {
  components: {
    CardProject,
  },
  data: () => ({
    projects: [],
  }),
  mounted() {
    this.getProjects();
  },
  methods: {
    async getProjects() {
      const res = await fetch(
        "https://crud-vue-d38b6-default-rtdb.firebaseio.com/projects.json"
      );
      const data = await res.json();

      for (let i in data) {
        //console.log(i);
        this.projects.push({
          id: i,
          data: data[i],
        });
      }

      console.log(this.projects);
    },
  },
};
</script>
