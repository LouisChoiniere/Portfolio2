<script lang="ts">
    import projectJson from "$lib/data/projects.json";
    import ProjectsGrid from "$lib/components/ProjectsGrid.svelte";

    let projects = $state(projectJson.sort((a, b) => a.id + b.id));
</script>

<h2>Projects</h2>

<ProjectsGrid {projects} />
