<script lang="ts">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import { faGithub, faLinkedin } from "@fortawesome/free-brands-svg-icons";

    import dataJson from "$lib/data/data.json";
    import projectJson from "$lib/data/projects.json";
    import ProjectsGrid from "$lib/components/ProjectsGrid.svelte";

    let data = $state(dataJson);
    let projects = $state(
        projectJson.filter((project) => project.isFeatured).sort((a, b) => a.id - b.id).reverse(),
    );
</script>

<h1>Louis Choinière</h1>

<p>
    {data.description}
</p>

<div class="links">
    <a href={data.links.linkedin} target="_blank" rel="noopener noreferrer">
        <FontAwesomeIcon icon={faLinkedin} size="sm" />LinkedIn
    </a>
    <span>|</span>
    <a href={data.links.github} target="_blank" rel="noopener noreferrer">
        <FontAwesomeIcon icon={faGithub} size="sm" />GitHub
    </a>
</div>

<h2>Resumé</h2>

<h2>Featured Projects</h2>

<ProjectsGrid {projects} />

<style lang="scss">
    .links {
        display: flex;
        gap: 0.5rem;

        a {
            text-decoration: none;
            color: inherit;
        }

        span {
            opacity: 0.65;
        };
    }
</style>
