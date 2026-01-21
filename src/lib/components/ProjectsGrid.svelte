<script lang="ts">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import { faGithub } from "@fortawesome/free-brands-svg-icons";
    import { faLink } from "@fortawesome/free-solid-svg-icons";

    let { projects } = $props();
</script>

<div class="cards">
    {#each projects as project}
        <div class="card">
            {#if project.image}
                <div class="card-image">
                    <img src={project.image} alt={project.title} />
                </div>
            {:else}
                <div>
                    <br />
                    <br />
                </div>
            {/if}
            <div class="card-body">
                <div class="title">
                    {project.title}

                    {#if project.links.site}
                        <a href={project.links.site} target="_blank" rel="noopener noreferrer">
                            <FontAwesomeIcon icon={faLink} size="sm" />
                        </a>
                    {/if}

                    {#if project.links.github}
                        <a href={project.links.github} target="_blank" rel="noopener noreferrer">
                            <FontAwesomeIcon icon={faGithub} size="sm" />
                        </a>
                    {/if}
                </div>
                <div class="date">{project.date}</div>
                <div class="description">{project.description}</div>
                <div class="tags">
                    {#each project.tags as tag}
                        <span class="tag colored">{tag}</span>
                    {/each}
                </div>
            </div>
        </div>
    {/each}
</div>

<style lang="scss">
    // @use "$lib/styles/components/_cards.scss" as cardStyles;
    // @use "$lib/styles/components/_tags.scss" as tagStyles;

    .cards {
        font-size: 0.8rem;
    }
</style>
