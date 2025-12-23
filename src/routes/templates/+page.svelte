<script lang="ts">
  import { onMount } from "svelte";
  import Default from "$lib/templates/default.svelte";
  import Minimal from "$lib/templates/minimal.svelte";
  import Tile from "$lib/templates/tile.svelte";
  import Modern from "$lib/templates/modern.svelte";
  import Classic from "$lib/templates/classic.svelte";
  import Executive from "$lib/templates/executive.svelte";
  import ATS from "$lib/templates/ats.svelte";
  import ModernPhoto from "$lib/templates/modern-photo.svelte";
  import SidebarPhoto from "$lib/templates/sidebar-photo.svelte";
  import CreativePhoto from "$lib/templates/creative-photo.svelte";
  import MinimalistPhoto from "$lib/templates/minimalist-photo.svelte";
  import CompactPhoto from "$lib/templates/compact-photo.svelte";

  let List = [
    { name: "default", component: Default },
    { name: "minimal", component: Minimal },
    { name: "tile", component: Tile },
    { name: "modern", component: Modern },
    { name: "classic", component: Classic },
    { name: "executive", component: Executive },
    { name: "ats", component: ATS },
    { name: "modern-photo", component: ModernPhoto },
    { name: "sidebar-photo", component: SidebarPhoto },
    { name: "creative-photo", component: CreativePhoto },
    { name: "minimalist-photo", component: MinimalistPhoto },
    { name: "compact-photo", component: CompactPhoto },
  ];

  onMount(() => document.body.style.overflow = "visible");
</script>

<div class="flex flex-wrap gap-(x4 y12) p10 justify-start items-start">
  {#each List as x}
    <div
      style="scale: 0.3; transform-origin: top left;"
      class="grid gap3 w-[63mm] h-[150mm] flex-shrink-0"
    >
      <a
        class="badge text-primary-fg w-full text-5xl h-fit p5 justify-center capitalize"
        href="/?theme={x.name}"
      >{x.name}</a>

      <div class="doc">
        <x.component />
      </div>
    </div>
  {/each}
</div>
