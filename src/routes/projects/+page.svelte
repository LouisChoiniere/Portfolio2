<script lang="ts">
    import projectJson from "$lib/data/projects.json";
    import ProjectsGrid from "$lib/components/ProjectsGrid.svelte";

    let projects = $state(projectJson.sort((a, b) => b.id - a.id));
</script>

<h2>Projects</h2>

<ProjectsGrid {projects} />
