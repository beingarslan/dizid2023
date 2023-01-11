<template>
  <div class="apps">
    <h1>Apps</h1>
    <p>Here are some of my apps:</p>
    <!-- <p>TEST: {{ state.projects }}</p> -->
    <div class="projects">
      <div v-for="project in state.projects" :key="project.id">
        <h2>{{ project.fields.Title }}</h2>
        <p>{{ project.fields.Excerpt }}</p>
        <p>{{ project.fields.URL }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";
import ProjectsService from "@/components/ProjectsService.js"; // use getProjects() from ProjectService to get all projects
let state = reactive(
  {
    projects: [],
  }
);
async function getProjects() {
  try {
    const response = await ProjectsService.getProjects().then((response) => {
      state.projects = response.data.records;
    });
  } catch (err) {
    console.log(err);
  }
}
getProjects();
</script>
