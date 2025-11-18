<!-- CREDIT -->
<!-- Text hover from https://landonorris.com/ -->
<!-- Recreated by Scott from Syntax team: https://www.youtube.com/watch?v=9H34nxxVEgc -->

<script>
  // plain Svelte reactivity (no runes)
  let sites = ["HELLO", "WORLD", "ANIMATION"];
  let active_font = "sans-serif";

  // values used in styles
  let size = 80; // px
  let weight = false; // toggles 100 vs 900
  let speed = 0.5; // seconds
</script>

<svelte:head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Svelte Animation</title>
</svelte:head>

<div
  class="app"
  style:--size={size + "px"}
  style:--font={active_font}
  style:--endWeight={weight ? "100" : "900"}
  style:--speed={speed + "s"}
>
  {#each sites as site}
    <span class="hover-text">
      {#each [...site] as text, i}
        <span style:--i={i}>{text}</span>
      {/each}
    </span>
  {/each}
</div>

<style>
  :global(body) {
    background: #000;
    min-height: 90vh;
  }

  div {
    font-family: var(--font), sans-serif;
    font-optical-sizing: auto;
    font-style: normal;
    text-align: center;
    align-content: center;
    min-height: 90vh;
  }

  .hover-text {
    text-shadow: 0 2ex 0;
    color: white;
    font-size: var(--size);
    text-transform: uppercase;
    font-variation-settings: "wght" 900;
    text-decoration: none;
    overflow: hidden;
    padding: 3px 0;
    line-height: 1;
    text-box-trim: both;
    text-box-edge: cap alphabetic;
    display: inline-block;
  }

  .hover-text span {
    position: relative;
    display: inline-block;
  }

  .hover-text:not(:hover) span {
    animation: down var(--speed) forwards;
    animation-delay: calc(var(--i) * 0.05s);
  }

  .hover-text:hover span {
    animation: up var(--speed) forwards;
    animation-delay: calc(var(--i) * 0.05s);
  }

  @keyframes up {
    100% {
      translate: 0 -2ex;
      font-variation-settings: "wght" var(--endWeight);
    }
  }

  @keyframes down {
    0% {
      translate: 0 -1.8ex;
    }
  }

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }
</style>
