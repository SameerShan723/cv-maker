<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-5xl mx-auto">
  <!-- Header with Sidebar -->
  <div class="grid grid-cols-[250px_1fr] gap-6 mb-6">
    <!-- Left Sidebar -->
    <div class="bg-primary text-primary-fg p-5 rounded">
      <h1 class="text-3xl font-bold mb-2 leading-tight">{data.details.name}</h1>
      <p class="text-sm mb-4 opacity-90">{data.details.role}</p>
      
      <div class="space-y-3 text-sm">
        <div class="frow gap-2">
          {@html icons.mail}
          <span class="break-all">{data.details.email}</span>
        </div>
        <div class="frow gap-2">
          {@html icons.phone}
          <span>{data.details.phone}</span>
        </div>
        {#if data.details.website}
          <div class="frow gap-2">
            {@html icons.globe}
            <a href={data.details.website} target="_blank" class="break-all underline">
              {formatUrl(data.details.website)}
            </a>
          </div>
        {/if}
        <div class="frow gap-2">
          {@html icons.github}
          <a href={`https://github.com/${data.details.github}`} target="_blank" class="underline">
            @{data.details.github}
          </a>
        </div>
      </div>
    </div>

    <!-- Right Content -->
    <div>
      <!-- Summary -->
      <section class="mb-6">
        <h2 class="text-xl font-bold mb-3 text-primary border-b-2 border-primary pb-1">Executive Summary</h2>
        <p class="text-sm leading-relaxed">{data.details.about}</p>
      </section>

      <!-- Work Experience -->
      <section class="mb-6">
        <h2 class="text-xl font-bold mb-3 text-primary border-b-2 border-primary pb-1">Professional Experience</h2>
        {#each data.workExp as work}
          <div class="mb-5">
            <div class="flex justify-between items-start mb-2">
              <div>
                <h3 class="text-lg font-semibold">{work.title}</h3>
                <p class="text-sm text-muted-fg font-medium">{work.company}</p>
              </div>
              <span class="text-xs text-muted-fg bg-secondary px-2 py-1 rounded">{work.date}</span>
            </div>
            <ul class="list-disc list-inside space-y-1 text-sm ml-2">
              {#each textAreaFormat(work?.desc ?? "") as line}
                <li>{line}</li>
              {/each}
            </ul>
          </div>
        {/each}
      </section>
    </div>
  </div>

  <!-- Bottom Section -->
  <div class="grid grid-cols-2 gap-6">
    <!-- Education -->
    <section>
      <h2 class="text-xl font-bold mb-3 text-primary border-b-2 border-primary pb-1">Education</h2>
      {#each data.education as edu}
        <div class="mb-4">
          <h3 class="font-semibold text-base">{edu.institution}</h3>
          <p class="text-sm text-muted-fg">{edu.qualification}</p>
          <p class="text-xs text-muted-fg">{edu.date}</p>
        </div>
      {/each}
    </section>

    <!-- Skills -->
    <section>
      <h2 class="text-xl font-bold mb-3 text-primary border-b-2 border-primary pb-1">Core Competencies</h2>
      <div class="flex flex-wrap gap-2">
        {#each data.skills as skill}
          <span class="badge-outline text-sm px-2 py-1">
            {#if skill.icon}
              <span class="inline-block mr-1">{@html skill.icon}</span>
            {/if}
            {skill.name}
          </span>
        {/each}
      </div>
    </section>
  </div>

  <!-- Projects -->
  {#if data.projects.length > 0}
    <section class="mt-6">
      <h2 class="text-xl font-bold mb-3 text-primary border-b-2 border-primary pb-1">Notable Projects</h2>
      <div class="grid grid-cols-2 gap-4">
        {#each data.projects as project}
          <div class="border border-fg p-3 rounded">
            <div class="flex justify-between items-start mb-2">
              <h3 class="font-semibold text-base">{project.name}</h3>
              <a href={project.link} target="_blank" class="text-primary text-xs">View →</a>
            </div>
            <p class="text-xs text-muted-fg">{project.desc}</p>
          </div>
        {/each}
      </div>
    </section>
  {/if}
</div>

