<script>
import axios from 'axios';

 export default {
    data(){
        return {
          projects: [],
          prevPage: null,
          nextPage: null,

        };
    },
    mounted() {
        this.getProjects();
    },
    methods: {
      getProjects() {
        axios
          .get('http://127.0.0.1:8000/api/projects')
          .then((res) => {
            console.log(res.data.projects);

            this.projects = res.data.projects.data;
            console.log(this.projects);

            this.prevPage = res.data.projects.prev_page_url;
            console.log(this.prevPage);
            this.nextPage = res.data.projects.next_page_url;
            console.log(this.nextPage);
          });
      },
      getPrevPage() {
        axios
          .get(this.prevPage)
          .then((res) => {
            console.log(res.data.projects);

            this.projects = res.data.projects.data;
            console.log(this.projects);

            this.prevPage = res.data.projects.prev_page_url;
            console.log(this.prevPage);
            this.nextPage = res.data.projects.next_page_url;
            console.log(this.nextPage);
          });
      },
      getNextPage() {
        axios
          .get(this.nextPage)
          .then((res) => {
            console.log(res.data.projects);

            this.projects = res.data.projects.data;
            console.log(this.projects);

            this.prevPage = res.data.projects.prev_page_url;
            console.log(this.prevPage);
            this.nextPage = res.data.projects.next_page_url;
            console.log(this.nextPage);
          });
      }
    }
 }
</script>

<template>
  <div class="container">
    <main>
      <div class="projects-container">
          <div v-for="project in projects" :key="project.id">
                <h3>
                  {{ project.name }}
                </h3>
                <h5 v-if="project.type != null">
                    {{ project.type.title }}
                </h5>
                <h5 v-else>
                    Progetto senza tipologia
                </h5>

                <div class="technologies-container">
                        <div v-for="technology in project.technologies" :key="technology.id" >
                            <h5>
                                {{ technology.name }}
                            </h5>
                           
                        </div>
                        <!-- <div v-for="technology in project.technologies" :key="technology.id" >
                            <h5 v-if=" technology != null">
                                {{ technology.name }}
                            </h5>
                            <h5 v-else>
                                 Progetto senza tecnologia
                            </h5>
                        </div> -->
                </div>
          </div>
      </div>
      <div class="buttons">
          <button @click="getPrevPage()">
            &lt; Precedente 
          </button>

          <button @click="getNextPage()">
            Successivo  &gt;
          </button>
      </div>
    </main>
  </div>
   
</template>

<style scoped>
    .projects-container{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }
    .projects-container > * {
        width: 30%;
        border: 2px solid lightgreen;
        margin-bottom: 10px ;
        padding: 5px;
    }
    .projects-container > * > h3{
        margin-bottom: 20px;
    }
    .projects-container > * > h5{
        margin-bottom: 10px;
    }
    .technologies-container > *{
      margin-bottom: 10px;

    }
   .technologies-container > * {
      background-color: lightgreen;
      border-radius: 50px;
      color: white;
      padding: 5px 8px;
    }
  .buttons{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .buttons > button{
    margin: 4px;
    padding: 6px 8px ;
    border: none;
    background-color: lightsalmon;
    border-radius: 20px;
    cursor: pointer;
    font-size: 1.4em;
    width: 100%;

  }

</style>
