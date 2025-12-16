<script lang="ts">
    import projectsdata from '$lib/projects.json';
    
    let projects = $state(projectsdata.filter(project => project.isFeatured).reverse());

</script>

<h1>Louis Choinière</h1>

<p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua.
</p>

<div>
    <a href="https://linkedin.com/in/louischoiniere">LinkedIn</a>
    <a href="https://github.com/louischoiniere">GitHub</a>
</div>

<h2>Resume</h2>

<h2>Projects</h2>

<div class="cards">
    {#each projects as project}
        <div class="card">
            <div class="card-image">
                <img src={project.image} alt={project.title} />
            </div>
            <div class="card-body">
                <div class="title">{project.title}</div>
                <div class="date">{project.date}</div>
                <div class="description">{project.description}</div>
                <div class="tags">
                    {#each project.tags as tag}
                        <span class="tag">{tag}</span>
                    {/each}
                </div>
            </div>
        </div>
    {/each}
</div>


<style lang="scss">
    .cards {
        font-size: 0.8rem;
    }
</style>