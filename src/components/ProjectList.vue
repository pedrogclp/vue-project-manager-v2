<template>
    <div id="app" v-cloak>
        <div class="sk-rotating-plane" v-if="projects.length === 0"></div>
        <div class="card m-3" v-for="project in projects" :key="project.id">
            <div class="card-header">
                Proyecto
            </div>
            <div class="card-body">
                <h5 class="card-title">{{ project.id }} # {{ project.title }}</h5>
                <p class="card-text">{{ project.description }}</p>
                <a href="#" class="btn btn-danger"
                    v-on:click="deleteProject(project)">Eliminar proyecto</a>
            </div>
            <div class="card-footer text-muted">
                {{ project.created_at | moment }}
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
export default {
    name : 'project-list',
    data() {
        return { projects: [] }
    },
    filters: {
        moment: (date) => {
            return moment(date).format('DD MMM YYYY');
        }
    },
    methods: {
        deleteProject : ( project ) => {
            console.warn( "Eliminar proyecto: ", project );
        }
    },
    mounted() {
        const serverURL = 'http://172.104.91.187/projects';
        const configAxios = {
            url: serverURL,
            method: 'get',
            responseType: 'json',
            data: {},
            headers: {
                'Content-type' : 'application/json',
                'Api-token': 'jJHGtk3IoZ84CmKlDz5N206w46yaj6v4mk0vXdTDl5w80iqnk0skp9Jp6NQ3'
            }
        }

        axios.request(configAxios).then( (response) => {
            console.log(response);
            this.projects = response.data;
        });
    }
}
</script>
<style>
    @import "https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css";
    @import "https://cdnjs.cloudflare.com/ajax/libs/spinkit/1.2.5/spinkit.min.css";
    [v-cloak] {
        display: none;
    }
</style>
