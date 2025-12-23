<script lang="ts">
  import icons from "$lib/icons";
  import { formatUrl, textAreaFormat } from "$lib/utils";
  import { data } from "$lib/state/index.svelte";
</script>

<div class="max-w-5xl mx-auto">
  <!-- Header with Photo -->
  <div class="bg-gradient-to-r from-primary to-primary/80 text-primary-fg p-8 rounded-t-lg mb-6">
    <div class="flex items-center gap-6">
      {#if data.details.photo}
        <div class="flex-shrink-0">
          <img
            src={data.details.photo}
            alt={data.details.name || "Profile Photo"}
            class="w-32 h-32 rounded-full object-cover border-4 border-primary-fg shadow-xl"
          />
        </div>
      {/if}
      <div class="flex-1">
        <h1 class="text-4xl font-bold mb-2">{data.details.name}</h1>
        <p class="text-xl opacity-90 mb-4">{data.details.role}</p>
        <div class="flex flex-wrap gap-4 text-sm">
          <span class="frow gap-1">{@html icons.mail} {data.details.email}</span>
          <span class="frow gap-1">{@html icons.phone} {data.details.phone}</span>
        </div>
      </div>
    </div>
  </div>

  <div class="grid grid-cols-[1fr_300px] gap-6">
    <!-- Main Content -->
    <div>
      <!-- Summary -->
      <section class="mb-6">
        <h2 class="text-2xl font-bold mb-3 text-primary border-l-4 border-primary pl-3">About Me</h2>
        <p class="text-sm leading-relaxed">{data.details.about}</p>
      </section>

      <!-- Work Experience -->
      <section class="mb-6">
        <h2 class="text-2xl font-bold mb-3 text-primary border-l-4 border-primary pl-3">Experience</h2>
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

      <!-- Projects -->
      {#if data.projects.length > 0}
        <section class="mb-6">
          <h2 class="text-2xl font-bold mb-3 text-primary border-l-4 border-primary pl-3">Projects</h2>
          {#each data.projects as project}
            <div class="mb-4 p-4 bg-secondary rounded-lg">
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
    </div>

    <!-- Sidebar -->
    <aside>
      <!-- Contact -->
      <section class="mb-6 p-4 bg-secondary rounded-lg">
        <h3 class="text-lg font-bold mb-3">Contact</h3>
        <div class="space-y-2 text-sm">
          {#if data.details.website}
            <a href={data.details.website} target="_blank" class="frow gap-2">
              {@html icons.globe} {formatUrl(data.details.website)}
            </a>
          {/if}
          <a href={`https://github.com/${data.details.github}`} target="_blank" class="frow gap-2">
            {@html icons.github} @{data.details.github}
          </a>
          {#if data.details.linkedin}
            <a href={data.details.linkedin} target="_blank" class="frow gap-2">
              {@html icons.link} LinkedIn
            </a>
          {/if}
        </div>
      </section>

      <!-- Education -->
      <section class="mb-6">
        <h3 class="text-lg font-bold mb-3 text-primary border-b-2 border-primary pb-1">Education</h3>
        {#each data.education as edu}
          <div class="mb-4">
            <h4 class="font-semibold text-base">{edu.institution}</h4>
            <p class="text-sm text-muted-fg">{edu.qualification}</p>
            <p class="text-xs text-muted-fg">{edu.date}</p>
          </div>
        {/each}
      </section>

      <!-- Skills -->
      <section>
        <h3 class="text-lg font-bold mb-3 text-primary border-b-2 border-primary pb-1">Skills</h3>
        <div class="flex flex-wrap gap-2">
          {#each data.skills as skill}
            <span class="badge-secondary px-2 py-1 text-xs">
              {#if skill.icon}
                <span class="inline-block mr-1">{@html skill.icon}</span>
              {/if}
              {skill.name}
            </span>
          {/each}
        </div>
      </section>
    </aside>
  </div>
</div>

