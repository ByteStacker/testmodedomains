<script>
  // @ts-nocheck

  import { onMount, afterUpdate } from "svelte";

  export let input = "";
  export let isPremium = false;
  export let isVip = true;

  let textElement;
  let wrapperElement;

  let fontSize = 40;
  const horizontalPadding = 20 * 2;

  onMount(() => {
    adjustFontSize();
  });

  afterUpdate(() => {
    adjustFontSize();
  });

  function adjustFontSize() {
    let parentWidth = wrapperElement.clientWidth - horizontalPadding;

    fontSize = 40;
    textElement.style.fontSize = `${fontSize}px`;
    while (textElement.scrollWidth > parentWidth && fontSize > 16) {
      fontSize--;
      textElement.style.fontSize = `${fontSize}px`;
    }
  }
</script>

<input
  type="text"
  bind:value={input}
  placeholder="Seed"
  maxlength="45"
  class="domain_input"
/>
<div class="wrapper" bind:this={wrapperElement} style="max-width: 600px;">
  <div class="content">
    <!-- <div class="overlay"></div> -->
    <slot />
  </div>
  <div
    class="text-wrapper"
    style="background-color: {isPremium ? '#dffe00' : '#000'}; color: {isPremium
      ? '#000'
      : '#fff'}"
  >
    <p bind:this={textElement} style="font-size: {fontSize}px">
      {input ? input + ".mode" : "" + ".mode"}
    </p>
  </div>
</div>

<style>
  div {
    background-color: #000;
    color: #fff;
    text-align: center;
    font-weight: 800;
    line-height: 100%;
  }
  .domain_input {
    margin: 20px 0;
  }
  .wrapper {
    border-radius: 20px;
    overflow: hidden;
    border: 1px solid white;
  }

  .content {
    height: 600px;
    width: 600px;
  }

  .text-wrapper {
    min-height: 80px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 0 20px;
    max-width: 600px;
    white-space: nowrap;
    text-transform: lowercase;
    line-height: 100%;
  }
</style>
