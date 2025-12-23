<script lang="ts">
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

  import Ui from "$lib/ui/index.svelte";
  import { page } from "$app/state";
  import { onMount } from "svelte";
  import { ui } from "$lib/state/index.svelte";

  let themes = {
    default: Default,
    minimal: Minimal,
    tile: Tile,
    modern: Modern,
    classic: Classic,
    executive: Executive,
    ats: ATS,
    "modern-photo": ModernPhoto,
    "sidebar-photo": SidebarPhoto,
    "creative-photo": CreativePhoto,
    "minimalist-photo": MinimalistPhoto,
    "compact-photo": CompactPhoto,
  };

  let Component = $derived(
    themes[(page.url.searchParams.get("theme")?.toLowerCase() as keyof typeof themes) || "default"],
  );

  onMount(() => {
    document.body.style.overflow = ui.mode == "split"
      ? "hidden"
      : "visible";
  });
</script>

<Ui>
  <Component />
</Ui>
