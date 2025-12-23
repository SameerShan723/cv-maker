<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-4xl mx-auto">
  <!-- Header -->
  <div class="text-center border-b-2 border-fg pb-4 mb-6">
    <h1 class="text-4xl font-bold uppercase tracking-wide mb-2">{data.details.name}</h1>
    <p class="text-lg text-muted-fg mb-3">{data.details.role}</p>
    <div class="flex flex-wrap justify-center gap-3 text-sm">
      <span>{data.details.email}</span>
      <span>•</span>
      <span>{data.details.phone}</span>
      {#if data.details.website}
        <span>•</span>
        <a href={data.details.website} target="_blank">{formatUrl(data.details.website)}</a>
      {/if}
      <span>•</span>
      <a href={`https://github.com/${data.details.github}`} target="_blank">GitHub</a>
    </div>
  </div>

  <!-- Summary -->
  <section class="mb-5">
    <h2 class="text-xl font-bold uppercase tracking-wide mb-2 border-b border-fg pb-1">Summary</h2>
    <p class="text-sm leading-relaxed">{data.details.about}</p>
  </section>

  <!-- Work Experience -->
  <section class="mb-5">
    <h2 class="text-xl font-bold uppercase tracking-wide mb-3 border-b border-fg pb-1">Professional Experience</h2>
    {#each data.workExp as work}
      <div class="mb-4">
        <div class="flex justify-between items-baseline mb-1">
          <div>
            <span class="font-semibold text-base">{work.title}</span>
            <span class="text-muted-fg">, {work.company}</span>
          </div>
          <span class="text-sm text-muted-fg italic">{work.date}</span>
        </div>
        <ul class="list-disc list-inside space-y-0.5 text-sm ml-4">
          {#each textAreaFormat(work?.desc ?? "") as line}
            <li>{line}</li>
          {/each}
        </ul>
      </div>
    {/each}
  </section>

  <!-- Education -->
  <section class="mb-5">
    <h2 class="text-xl font-bold uppercase tracking-wide mb-3 border-b border-fg pb-1">Education</h2>
    {#each data.education as edu}
      <div class="mb-3">
        <div class="flex justify-between items-baseline">
          <div>
            <span class="font-semibold text-base">{edu.institution}</span>
            <span class="text-muted-fg"> — {edu.qualification}</span>
          </div>
          <span class="text-sm text-muted-fg italic">{edu.date}</span>
        </div>
      </div>
    {/each}
  </section>

  <!-- Skills -->
  <section class="mb-5">
    <h2 class="text-xl font-bold uppercase tracking-wide mb-3 border-b border-fg pb-1">Technical Skills</h2>
    <p class="text-sm">
      {data.skills.map((s) => s.name).join(" • ")}
    </p>
  </section>

  <!-- Projects -->
  {#if data.projects.length > 0}
    <section class="mb-5">
      <h2 class="text-xl font-bold uppercase tracking-wide mb-3 border-b border-fg pb-1">Projects</h2>
      {#each data.projects as project}
        <div class="mb-3">
          <div class="flex justify-between items-baseline mb-1">
            <span class="font-semibold text-base">{project.name}</span>
            <a href={project.link} target="_blank" class="text-sm text-primary">Link</a>
          </div>
          <p class="text-sm text-muted-fg ml-4">{project.desc}</p>
        </div>
      {/each}
    </section>
  {/if}
</div>

