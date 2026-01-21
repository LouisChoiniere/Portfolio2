<script lang="ts">
  import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
  import { faGithub, faLinkedin } from "@fortawesome/free-brands-svg-icons";
  import { faEnvelope, faLocationDot } from "@fortawesome/free-solid-svg-icons";

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

  function getTimeSinceStart(startDate: string): string {
    const diffMs = new Date().getTime() - new Date(startDate).getTime();
    const years = Math.floor(diffMs / (1000 * 60 * 60 * 24 * 365.25));

    if (years !== 0) {
      return ` (${years} ${years === 1 ? "year" : "years"})`;
    }

    const months = Math.floor(diffMs / (1000 * 60 * 60 * 24 * 30.44));
    if (months !== 0) {
      return ` (${months} ${months === 1 ? "month" : "months"})`;
    }

    return "";
  }
</script>

<h1 class="name">Louis Choinière</h1>
<div class="subtitle">
  <span>
    <FontAwesomeIcon icon={faLocationDot} size="sm" /> {data.location}
  </span>
  <span>
    <FontAwesomeIcon icon={faEnvelope} size="sm" /> <a href="mailto:{data.mail}">{data.mail}</a>
  </span>
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

<hr />

<h2>Employment</h2>
<div class="employment">
  {#each data.employment as employment}
    <div class="employer">
      <div class="header">
        <span class="title">{employment.company}</span>
      </div>
      {#if employment.description}
        <span class="desc">{employment.description}</span>
      {/if}
    </div>
    {#each employment.segments as segment}
      <div class="position {'current' in segment && segment.current ? 'hollow' : ''}">
        <div class="header">
          <span class="title">{segment.position}</span>
          <span class="meta">{segment.dates}{"start_date" in segment ? getTimeSinceStart(segment.start_date) : ""}</span
          >
        </div>
        {#if segment.description}
          <div class="desc">{segment.description}</div>
        {/if}
      </div>
    {/each}
  {/each}
</div>

<hr />

<h2>Education</h2>
<div class="education">
  {#each data.education as education}
    <div class="education-item {'current' in education && education.current ? 'hollow' : ''}">
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

<hr />

<h2>Featured Projects</h2>
<p>
  A selection of projects that I have worked on recently. For a more comprehensive list, please visit the Projects page.
</p>
<p>
  <em>Note: Still working on adding past projects.</em>
</p>
<ProjectsGrid {projects} />

<style lang="scss">
  @use "$lib/styles/pallet.scss" as *;
  @use "$lib/styles/_responsive.scss" as rs;
  @use "$lib/styles/helpers/graph.scss" as graph;

  .name {
    margin-bottom: 0;

    font-size: 2.5rem;
  }

  .subtitle {
    margin-top: 0;

    font-size: 0.9rem;
    opacity: 0.75;

    display: flex;
    gap: 1rem;

    @include rs.is-mobile {
      flex-direction: column;
      gap: 0.25rem;
    }

    span {
      white-space: nowrap;
    }
  }

  .links {
    display: flex;
    gap: 0.5rem;

    span {
      opacity: 0.65;
    }
  }

  hr {
    margin: 2rem 0;
    border: none;
    border-top: 2px solid $shade2;
  }

  h2 {
    margin-bottom: 1rem;
  }

  .employment,
  .education {
    .header {
      margin-bottom: 0.25rem;

      display: flex;
      justify-content: space-between;
      align-items: baseline;

      @include rs.is-less-than-medium {
        flex-direction: column;
        align-items: flex-start;

        > .meta {
          margin-left: 0 !important;
          margin-top: 0.25rem;
        }
      }

      &:only-child {
        margin-bottom: 0;
      }

      > .title {
        font-size: 1.1rem;
        color: $shade7;
      }

      > .meta {
        margin-left: 1rem;

        font-size: 0.85rem;
        font-style: italic;
        white-space: nowrap;
        color: $shade5;
      }
    }

    .desc {
      font-size: 0.95rem;
      color: $shade6;
    }
  }

  .employment {
    > .employer {
      @include graph.graph-no-line();

      padding-bottom: 0.75rem;

      &:not(:first-child) {
        @include graph.graph-no-dot($graph-color, $shade0);
        padding-top: 1.5rem;
      }

      > .header > .title {
        font-weight: bold;
        font-size: 1.25rem;
      }
    }

    > .position {
      padding-bottom: 0.75rem;

      &:nth-child(2) {
        @include graph.graph-start($graph-color, $shade0);
      }

      &:nth-child(n + 3) {
        @include graph.graph($graph-color, $shade0);
      }
    }
  }

  .education > .education-item {
    @include graph.graph($graph-color, $shade0);

    &:not(:last-child) {
      padding-bottom: 1rem;
    }

    margin-bottom: 1.5rem;
  }
</style>
