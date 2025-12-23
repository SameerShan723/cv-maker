<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-4xl mx-auto">
  <!-- Header with Photo -->
  <div class="flex gap-6 mb-6 pb-6 border-b-4 border-primary">
    {#if data.details.photo}
      <div class="flex-shrink-0">
        <img
          src={data.details.photo}
          alt={data.details.name || "Profile Photo"}
          class="w-32 h-32 rounded-full object-cover border-4 border-primary"
        />
      </div>
    {/if}
    <div class="flex-1">
      <h1 class="text-5xl font-bold mb-2">{data.details.name}</h1>
      <p class="text-xl text-muted-fg mb-4">{data.details.role}</p>
      
      <div class="flex flex-wrap gap-4 text-sm">
        <span class="frow gap-1">{@html icons.mail} {data.details.email}</span>
        <span class="frow gap-1">{@html icons.phone} {data.details.phone}</span>
        {#if data.details.website}
          <a class="frow gap-1" href={data.details.website} target="_blank">
            {@html icons.globe} {formatUrl(data.details.website)}
          </a>
        {/if}
        <a class="frow gap-1" href={`https://github.com/${data.details.github}`} target="_blank">
          {@html icons.github} @{data.details.github}
        </a>
        {#if data.details.linkedin}
          <a class="frow gap-1" href={data.details.linkedin} target="_blank">
            {@html icons.link} LinkedIn
          </a>
        {/if}
      </div>
    </div>
  </div>

  <!-- Professional Summary -->
  <section class="mb-6">
    <h2 class="text-2xl font-bold mb-3 border-l-4 border-primary pl-3">Professional Summary</h2>
    <p class="text-sm leading-relaxed">{data.details.about}</p>
  </section>

  <!-- Work Experience -->
  <section class="mb-6">
    <h2 class="text-2xl font-bold mb-3 border-l-4 border-primary pl-3">Work Experience</h2>
    {#each data.workExp as work}
      <div class="mb-5">
        <div class="flex justify-between items-start mb-2">
          <div>
            <h3 class="text-lg font-semibold">{work.title}</h3>
            <p class="text-base text-muted-fg">{work.company}</p>
          </div>
          <span class="text-sm text-muted-fg whitespace-nowrap ml-4">{work.date}</span>
        </div>
        <ul class="list-disc list-inside space-y-1 text-sm ml-2">
          {#each textAreaFormat(work?.desc ?? "") as line}
            <li>{line}</li>
          {/each}
        </ul>
      </div>
    {/each}
  </section>

  <!-- Education -->
  <section class="mb-6">
    <h2 class="text-2xl font-bold mb-3 border-l-4 border-primary pl-3">Education</h2>
    {#each data.education as edu}
      <div class="mb-4">
        <div class="flex justify-between items-start mb-1">
          <div>
            <h3 class="text-lg font-semibold">{edu.institution}</h3>
            <p class="text-sm text-muted-fg">{edu.qualification}</p>
          </div>
          <span class="text-sm text-muted-fg">{edu.date}</span>
        </div>
      </div>
    {/each}
  </section>

  <!-- Skills -->
  <section class="mb-6">
    <h2 class="text-2xl font-bold mb-3 border-l-4 border-primary pl-3">Skills</h2>
    <div class="flex flex-wrap gap-2">
      {#each data.skills as skill}
        <span class="badge-secondary px-3 py-1 text-sm">
          {#if skill.icon}
            <span class="inline-block mr-1">{@html skill.icon}</span>
          {/if}
          {skill.name}
        </span>
      {/each}
    </div>
  </section>

  <!-- Projects -->
  {#if data.projects.length > 0}
    <section class="mb-6">
      <h2 class="text-2xl font-bold mb-3 border-l-4 border-primary pl-3">Projects</h2>
      {#each data.projects as project}
        <div class="mb-4 pb-4 border-b border-fg last:border-0">
          <div class="flex justify-between items-start mb-2">
            <h3 class="text-lg font-semibold">{project.name}</h3>
            <a href={project.link} target="_blank" class="text-primary text-sm hover:underline">
              View Project →
            </a>
          </div>
          <p class="text-sm text-muted-fg">{project.desc}</p>
        </div>
      {/each}
    </section>
  {/if}
</div>

