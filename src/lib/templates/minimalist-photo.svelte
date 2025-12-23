<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-4xl mx-auto">
  <!-- Header -->
  <div class="flex justify-between items-start mb-8 pb-6 border-b-2 border-fg">
    <div class="flex-1">
      <h1 class="text-4xl font-light mb-2">{data.details.name}</h1>
      <p class="text-lg text-muted-fg mb-4">{data.details.role}</p>
      <div class="flex flex-wrap gap-4 text-sm text-muted-fg">
        <span>{data.details.email}</span>
        <span>•</span>
        <span>{data.details.phone}</span>
        {#if data.details.website}
          <span>•</span>
          <a href={data.details.website} target="_blank">{formatUrl(data.details.website)}</a>
        {/if}
      </div>
    </div>
    {#if data.details.photo}
      <div class="ml-6 flex-shrink-0">
        <img
          src={data.details.photo}
          alt={data.details.name || "Profile Photo"}
          class="w-24 h-24 rounded-full object-cover border-2 border-fg"
        />
      </div>
    {/if}
  </div>

  <!-- Summary -->
  <section class="mb-8">
    <h2 class="text-xl font-light uppercase tracking-wider mb-3">Summary</h2>
    <p class="text-sm leading-relaxed text-muted-fg">{data.details.about}</p>
  </section>

  <!-- Work Experience -->
  <section class="mb-8">
    <h2 class="text-xl font-light uppercase tracking-wider mb-4">Experience</h2>
    {#each data.workExp as work}
      <div class="mb-6">
        <div class="flex justify-between items-baseline mb-2">
          <div>
            <span class="font-medium text-base">{work.title}</span>
            <span class="text-muted-fg">, {work.company}</span>
          </div>
          <span class="text-xs text-muted-fg">{work.date}</span>
        </div>
        <ul class="list-disc list-inside space-y-1 text-sm text-muted-fg ml-4">
          {#each textAreaFormat(work?.desc ?? "") as line}
            <li>{line}</li>
          {/each}
        </ul>
      </div>
    {/each}
  </section>

  <!-- Education -->
  <section class="mb-8">
    <h2 class="text-xl font-light uppercase tracking-wider mb-4">Education</h2>
    {#each data.education as edu}
      <div class="mb-4">
        <div class="flex justify-between items-baseline">
          <div>
            <span class="font-medium text-base">{edu.institution}</span>
            <span class="text-muted-fg">, {edu.qualification}</span>
          </div>
          <span class="text-xs text-muted-fg">{edu.date}</span>
        </div>
      </div>
    {/each}
  </section>

  <!-- Skills -->
  <section class="mb-8">
    <h2 class="text-xl font-light uppercase tracking-wider mb-4">Skills</h2>
    <p class="text-sm text-muted-fg">
      {data.skills.map((s) => s.name).join(" / ")}
    </p>
  </section>

  <!-- Projects -->
  {#if data.projects.length > 0}
    <section class="mb-8">
      <h2 class="text-xl font-light uppercase tracking-wider mb-4">Projects</h2>
      {#each data.projects as project}
        <div class="mb-4">
          <div class="flex justify-between items-baseline mb-1">
            <span class="font-medium text-base">{project.name}</span>
            <a href={project.link} target="_blank" class="text-xs text-muted-fg hover:text-primary">
              Link
            </a>
          </div>
          <p class="text-sm text-muted-fg">{project.desc}</p>
        </div>
      {/each}
    </section>
  {/if}
</div>

