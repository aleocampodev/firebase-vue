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
      <form @submit.prevent="createdProject" class="col s12">
        <div class="row">
          <div class="input-field col s12">
            <input
              id="first_name"
              type="text"
              class="validate"
              v-model="project.title"
            />
            <label for="first_name">Nombre del Proyecto</label>
          </div>
          <div class="input-field col s12">
            <input
              id="last_name"
              type="text"
              class="validate"
              v-model="project.description"
            />
            <label for="last_name">Descripcion del Proyecto</label>
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
  data: () => ({
    project: {
      title: "",
      description: "",
      langs: [],
      status: true,
    },
  }),
  methods: {
    async createdProject() {
      await fetch(
        "https://crud-vue-d38b6-default-rtdb.firebaseio.com/projects.json",
        {
          method: "POST",
          body: JSON.stringify(this.project),
        }
      );
      this.project = {};
    },
  },
};
</script>
