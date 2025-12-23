<script lang="ts">
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-4xl mx-auto">
  <!-- Simple Header -->
  <div class="mb-6">
    <h1 class="text-4xl font-bold mb-1">{data.details.name}</h1>
    <p class="text-lg text-muted-fg mb-3">{data.details.role}</p>
    <div class="text-sm space-y-1">
      <p>{data.details.email} | {data.details.phone}</p>
      {#if data.details.website}
        <p>{formatUrl(data.details.website)}</p>
      {/if}
      <p>GitHub: github.com/{data.details.github}</p>
    </div>
  </div>

  <!-- Summary -->
  <section class="mb-5">
    <h2 class="text-xl font-bold mb-2">PROFESSIONAL SUMMARY</h2>
    <hr class="border-fg mb-2" />
    <p class="text-sm">{data.details.about}</p>
  </section>

  <!-- Work Experience -->
  <section class="mb-5">
    <h2 class="text-xl font-bold mb-2">PROFESSIONAL EXPERIENCE</h2>
    <hr class="border-fg mb-2" />
    {#each data.workExp as work}
      <div class="mb-4">
        <div class="flex justify-between items-baseline mb-1">
          <div>
            <span class="font-semibold text-base">{work.title}</span>
            <span class="text-muted-fg"> | {work.company}</span>
          </div>
          <span class="text-sm">{work.date}</span>
        </div>
        <ul class="list-disc list-inside text-sm ml-4 space-y-0.5">
          {#each textAreaFormat(work?.desc ?? "") as line}
            <li>{line}</li>
          {/each}
        </ul>
      </div>
    {/each}
  </section>

  <!-- Education -->
  <section class="mb-5">
    <h2 class="text-xl font-bold mb-2">EDUCATION</h2>
    <hr class="border-fg mb-2" />
    {#each data.education as edu}
      <div class="mb-3">
        <div class="flex justify-between items-baseline">
          <div>
            <span class="font-semibold text-base">{edu.institution}</span>
            <span class="text-muted-fg">, {edu.qualification}</span>
          </div>
          <span class="text-sm">{edu.date}</span>
        </div>
      </div>
    {/each}
  </section>

  <!-- Skills -->
  <section class="mb-5">
    <h2 class="text-xl font-bold mb-2">TECHNICAL SKILLS</h2>
    <hr class="border-fg mb-2" />
    <p class="text-sm">
      {data.skills.map((s) => s.name).join(", ")}
    </p>
  </section>

  <!-- Projects -->
  {#if data.projects.length > 0}
    <section class="mb-5">
      <h2 class="text-xl font-bold mb-2">PROJECTS</h2>
      <hr class="border-fg mb-2" />
      {#each data.projects as project}
        <div class="mb-3">
          <div class="flex justify-between items-baseline mb-1">
            <span class="font-semibold text-base">{project.name}</span>
            <a href={project.link} target="_blank" class="text-sm text-primary">Link</a>
          </div>
          <p class="text-sm text-muted-fg">{project.desc}</p>
        </div>
      {/each}
    </section>
  {/if}
</div>

