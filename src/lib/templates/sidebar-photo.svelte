<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-5xl mx-auto grid grid-cols-[280px_1fr] gap-6">
  <!-- Left Sidebar -->
  <aside class="bg-primary text-primary-fg p-6 rounded-lg">
    {#if data.details.photo}
      <div class="mb-6 text-center">
        <img
          src={data.details.photo}
          alt={data.details.name || "Profile Photo"}
          class="w-40 h-40 rounded-full object-cover mx-auto border-4 border-primary-fg shadow-lg"
        />
      </div>
    {/if}

    <h1 class="text-3xl font-bold mb-2 text-center">{data.details.name}</h1>
    <p class="text-sm mb-6 text-center opacity-90">{data.details.role}</p>

    <!-- Contact Info -->
    <div class="space-y-4 mb-6">
      <h3 class="text-lg font-bold uppercase tracking-wide border-b border-primary-fg pb-2">Contact</h3>
      <div class="space-y-3 text-sm">
        <div class="frow gap-2">
          {@html icons.mail}
          <span class="break-all">{data.details.email}</span>
        </div>
        <div class="frow gap-2">
          {@html icons.phone}
          <span>{data.details.phone}</span>
        </div>
        {#if data.details.location}
          <div class="frow gap-2">
            {@html icons.location}
            <span>{data.details.location}</span>
          </div>
        {/if}
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
        {#if data.details.linkedin}
          <div class="frow gap-2">
            {@html icons.link}
            <a href={data.details.linkedin} target="_blank" class="underline">LinkedIn</a>
          </div>
        {/if}
      </div>
    </div>

    <!-- Skills -->
    <div class="mb-6">
      <h3 class="text-lg font-bold uppercase tracking-wide border-b border-primary-fg pb-2 mb-3">Skills</h3>
      <div class="space-y-2">
        {#each data.skills as skill}
          <div class="text-sm">
            {#if skill.icon}
              <span class="inline-block mr-2">{@html skill.icon}</span>
            {/if}
            {skill.name}
          </div>
        {/each}
      </div>
    </div>
  </aside>

  <!-- Main Content -->
  <main>
    <!-- Summary -->
    <section class="mb-6">
      <h2 class="text-2xl font-bold mb-3 text-primary border-b-2 border-primary pb-2">Professional Summary</h2>
      <p class="text-sm leading-relaxed">{data.details.about}</p>
    </section>

    <!-- Work Experience -->
    <section class="mb-6">
      <h2 class="text-2xl font-bold mb-3 text-primary border-b-2 border-primary pb-2">Work Experience</h2>
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

    <!-- Education -->
    <section class="mb-6">
      <h2 class="text-2xl font-bold mb-3 text-primary border-b-2 border-primary pb-2">Education</h2>
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

    <!-- Projects -->
    {#if data.projects.length > 0}
      <section class="mb-6">
        <h2 class="text-2xl font-bold mb-3 text-primary border-b-2 border-primary pb-2">Projects</h2>
        {#each data.projects as project}
          <div class="mb-4 pb-4 border-b border-fg last:border-0">
            <div class="flex justify-between items-start mb-2">
              <h3 class="text-lg font-semibold">{project.name}</h3>
              <a href={project.link} target="_blank" class="text-primary text-sm hover:underline">
                View →
              </a>
            </div>
            <p class="text-sm text-muted-fg">{project.desc}</p>
          </div>
        {/each}
      </section>
    {/if}
  </main>
</div>

