<script lang="ts">
  import prompts from '../prompts/prompts.csv'

  const inputPrompt = (prompt: string) => {
    input.value = prompt
    input.style.height = 'auto'
    input.style.height = input.scrollHeight + 'px'
    active = false
  }

  export let input : HTMLTextAreaElement

  let active: boolean = false
</script>

{#if input}
<div class="columns is-centered">
  <div class="column is-half">
    <div class="dropdown is-fullwidth" class:is-active={active}>
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <div class="dropdown-trigger" on:click={() => { active = !active }}>
        <button class="button is-fullwidth" aria-haspopup="true" aria-controls="dropdown-menu">
          <span>选择预设情景</span>
          <span class="icon is-small">👇</span>
        </button>
      </div>
      <div class="dropdown-menu" id="dropdown-menu" role="menu">
        <div class="dropdown-content">
          {#each prompts as prompt}
            <a title={prompt.prompt} class="dropdown-item" href={'#'} on:click|preventDefault={() => inputPrompt(prompt.prompt)}>
              {prompt.act}
            </a>
          {/each}
        </div>
      </div>
    </div>
  </div>
</div>

<div class="columns is-centered">
  <div class="column is-half has-text-centered">或在下方填写：</div>
</div>
{/if}