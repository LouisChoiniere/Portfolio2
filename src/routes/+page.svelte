<script lang="ts">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import { faGithub, faLinkedin } from "@fortawesome/free-brands-svg-icons";
    import {
        faEnvelope,
        faLocationDot,
    } from "@fortawesome/free-solid-svg-icons";

    import dataJson from "$lib/data/data.json";
    import projectJson from "$lib/data/projects.json";
    import ProjectsGrid from "$lib/components/ProjectsGrid.svelte";

    let data = $state(dataJson);
    let projects = $state(
        projectJson
            .filter((project) => project.isFeatured)
            .sort((a, b) => a.id - b.id)
            .reverse(),
    );
</script>

<h1 class="name">Louis Choinière</h1>
<div class="subtitle">
    <FontAwesomeIcon icon={faLocationDot} size="sm" />
    {data.location}. &nbsp;&nbsp;
    <FontAwesomeIcon icon={faEnvelope} size="sm" />
    <a href="mailto:{data.mail}">{data.mail}</a>
</div>

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

<h2>Employment</h2>
<div class="info-list">
    {#each data.employment as employment}
        <div class="info-item">
            <div class="header">
                <span class="title">{employment.company}</span>
            </div>
            {#if employment.description}
                <span class="desc">{employment.description}</span>
            {/if}
            <div class="list">
                {#each employment.segments as segment}
                    <div class="info-item">
                        <div class="header">
                            <span class="title">{segment.position}</span>
                            <span class="meta">{segment.dates}</span>
                        </div>
                        {#if segment.description}
                            <div class="desc">{segment.description}</div>
                        {/if}
                    </div>
                {/each}
            </div>
        </div>
    {/each}
</div>

<h2>Education</h2>
<div class="info-list">
    {#each data.education as education}
        <div class="info-item">
            <div class="header">
                <span class="title">{education.degree}</span>
                <span class="meta">
                    {education.institution} &middot; {education.dates}
                </span>
            </div>
            <div class="desc">
                {education.description}
            </div>
        </div>
    {/each}
</div>

<h2>Featured Projects</h2>

<ProjectsGrid {projects} />

<style lang="scss">
    .name {
        margin-bottom: 0;

        font-size: 1.75rem;
    }

    .subtitle {
        margin-top: 0;

        font-size: 0.8rem;
        opacity: 0.75;
    }

    .links {
        display: flex;
        gap: 0.5rem;

        span {
            opacity: 0.65;
        }
    }

    h2 {
        margin-top: 2.5rem;
        margin-bottom: 1rem;
    }
</style>
