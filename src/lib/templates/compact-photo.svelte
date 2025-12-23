<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-4xl mx-auto">
  <!-- Compact Header with Photo -->
  <div class="flex gap-4 mb-6 pb-4 border-b-2 border-primary">
    {#if data.details.photo}
      <img
        src={data.details.photo}
        alt={data.details.name || "Profile Photo"}
        class="w-20 h-20 rounded object-cover border-2 border-primary flex-shrink-0"
      />
    {/if}
    <div class="flex-1">
      <h1 class="text-3xl font-bold mb-1">{data.details.name}</h1>
      <p class="text-base text-muted-fg mb-2">{data.details.role}</p>
      <div class="flex flex-wrap gap-3 text-xs">
        <span>{data.details.email}</span>
        <span>|</span>
        <span>{data.details.phone}</span>
        {#if data.details.website}
          <span>|</span>
          <a href={data.details.website} target="_blank">{formatUrl(data.details.website)}</a>
        {/if}
        <span>|</span>
        <a href={`https://github.com/${data.details.github}`} target="_blank">GitHub</a>
      </div>
    </div>
  </div>

  <!-- Two Column Layout -->
  <div class="grid grid-cols-[2fr_1fr] gap-6">
    <!-- Left Column -->
    <div>
      <!-- Summary -->
      <section class="mb-5">
        <h2 class="text-lg font-bold mb-2 uppercase tracking-wide">Summary</h2>
        <p class="text-xs leading-relaxed">{data.details.about}</p>
      </section>

      <!-- Work Experience -->
      <section class="mb-5">
        <h2 class="text-lg font-bold mb-3 uppercase tracking-wide">Experience</h2>
        {#each data.workExp as work}
          <div class="mb-4">
            <div class="flex justify-between items-start mb-1">
              <div>
                <span class="font-semibold text-sm">{work.title}</span>
                <span class="text-xs text-muted-fg"> - {work.company}</span>
              </div>
              <span class="text-xs text-muted-fg">{work.date}</span>
            </div>
            <ul class="list-disc list-inside space-y-0.5 text-xs ml-2">
              {#each textAreaFormat(work?.desc ?? "") as line}
                <li>{line}</li>
              {/each}
            </ul>
          </div>
        {/each}
      </section>

      <!-- Projects -->
      {#if data.projects.length > 0}
        <section class="mb-5">
          <h2 class="text-lg font-bold mb-3 uppercase tracking-wide">Projects</h2>
          {#each data.projects as project}
            <div class="mb-3">
              <div class="flex justify-between items-start mb-1">
                <span class="font-semibold text-sm">{project.name}</span>
                <a href={project.link} target="_blank" class="text-xs text-primary">Link</a>
              </div>
              <p class="text-xs text-muted-fg">{project.desc}</p>
            </div>
          {/each}
        </section>
      {/if}
    </div>

    <!-- Right Column -->
    <div>
      <!-- Education -->
      <section class="mb-5">
        <h2 class="text-lg font-bold mb-3 uppercase tracking-wide">Education</h2>
        {#each data.education as edu}
          <div class="mb-3">
            <h4 class="font-semibold text-sm">{edu.institution}</h4>
            <p class="text-xs text-muted-fg">{edu.qualification}</p>
            <p class="text-xs text-muted-fg">{edu.date}</p>
          </div>
        {/each}
      </section>

      <!-- Skills -->
      <section>
        <h2 class="text-lg font-bold mb-3 uppercase tracking-wide">Skills</h2>
        <div class="space-y-1">
          {#each data.skills as skill}
            <div class="text-xs">
              {#if skill.icon}
                <span class="inline-block mr-1">{@html skill.icon}</span>
              {/if}
              {skill.name}
            </div>
          {/each}
        </div>
      </section>
    </div>
  </div>
</div>

