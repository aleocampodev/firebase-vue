<template>
  <div class="container">
    <div class="row">
      <router-link
        to="/proyectos"
        class="col s12 waves-effect waves-light btn amber darken-3"
      >
        <i class="material-icons">arrow_back</i>
        Regresar a la lista
      </router-link>
    </div>
    <div class="row">
      <form class="col s12" @submit.prevent="updatedProject">
        <div class="row">
          <div class="input-field col s12">
            <input
              id="first_name"
              type="text"
              class="validate"
              v-model="project.title"
              placeholder="Nombre del proyecto"
            />
            <label for="first_name"></label>
          </div>
          <div class="input-field col s12">
            <input
              id="last_name"
              type="text"
              class="validate"
              v-model="project.description"
              placeholder="Descripcion del proyectos"
            />
            <label for="last_name"></label>
          </div>
          <p>
            <label>
              <input
                type="checkbox"
                checked="checked"
                value="html"
                v-model="project.langs"
              />
              <span>HTML</span>
            </label>
          </p>
          <p>
            <label>
              <input
                type="checkbox"
                checked="checked"
                value="css"
                v-model="project.langs"
              />
              <span>CSS</span>
            </label>
          </p>
          <p>
            <label>
              <input
                type="checkbox"
                checked="checked"
                value="javascript"
                v-model="project.langs"
              />
              <span>JavaScript</span>
            </label>
          </p>
          <p>
            <label>
              <input
                type="checkbox"
                checked="checked"
                value="vue"
                v-model="project.langs"
              />
              <span>Vue</span>
            </label>
          </p>
          <button
            class="btn waves-effect waves-light"
            type="submit"
            name="action"
            col
            s12
          >
            Submit
            <i class="material-icons right">send</i>
          </button>
        </div>
      </form>
    </div>
    {{ project }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      project: {},
      id: this.$route.params.id,
    };
  },
  mounted() {
    this.getProject();
  },
  methods: {
    async getProject() {
      //const id = this.$route.params.id;
      //console.log(id);
      const res = await fetch(
        `https://crud-vue-d38b6-default-rtdb.firebaseio.com/projects/${this.id}.json`
      );

      const data = await res.json();
      this.project = data;
      console.log(this.$route.params.id);
    },
    async updatedProject() {
      const res = await fetch(
        `https://crud-vue-d38b6-default-rtdb.firebaseio.com/projects/${this.id}.json`,
        {
          method: "PATCH",
          body: JSON.stringify(this.project),
        }
      );

      const data = await res.json();

      this.data.data.status = data["status"];

      console.log(data);
    },
  },
};
</script>
