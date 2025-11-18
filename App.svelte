<!-- CREDIT -->
<!-- Text hover from https://landonorris.com/ -->
<!-- Recreated by Scott from Syntax team: https://www.youtube.com/watch?v=9H34nxxVEgc -->

<script>
  let sites = $state(["HELLO", "WORLD", "ANIMATION"]);
  let active_font = $state("sans-serif");
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
    <a
      >{#each [...site] as text, i}<span style:--i={i}>{text}</span>{/each}</a
    >
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

  a {
    text-shadow: 0 2ex 0;
    color: red;
    font-size: var(--size);
    text-transform: uppercase;
    font-variation-settings: "wght" 900;
    text-decoration: none;
    overflow: hidden;
    padding: 3px 0;
    line-height: 1;
    text-box-trim: both;
    text-box-edge: cap alphabetic;
  }

  a span {
    position: relative;
    display: inline-block;
  }

  a:not(:hover) span {
    animation: down var(--speed) forwards;
    animation-delay: calc(var(--i) * 0.05s);
  }

  a:hover span {
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
