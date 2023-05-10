<script lang="ts">
  import { apiKeyStorage } from './Storage.svelte'

  $: apiKey = $apiKeyStorage
</script>

<article class="message">
  <div class="message-body">
    <strong><a href="https://github.com/Niek/chatgpt-web">ChatGLM-emailgen-web</a></strong>
    是一个简单的web展示chatGLM邮件信息填充的web应用
  </div>
</article>
<article class="message" class:is-danger={!apiKey} class:is-warning={apiKey}>
  <div class="message-body">
    在下方设置您的API key:
    <form
      class="field has-addons has-addons-right"
      on:submit|preventDefault={(event) => {
        if (event.target && event.target[0].value) {
        apiKeyStorage.set(event.target[0].value)
        }
      }}
    >
      <p class="control is-expanded">
        <input
          aria-label="OpenAI API key"
          type="password"
          autocomplete="off"
          class="input"
          class:is-danger={!apiKey}
          value={apiKey}
        />
      </p>
      <p class="control">
        <button class="button is-info" type="submit">保存</button>
      </p>
    </form>

    {#if !apiKey}
      <p class="help is-danger">
        请输入您的 <a href="https://platform.openai.com/account/api-keys">API key</a> 来使用 ChatGLM-emailgen-web.
      </p>
    {/if}
  </div>
</article>
{#if apiKey}
  <article class="message is-info">
    <div class="message-body">
      选择已有的邮件, 或
      <a href={'#/chat/new'}>创建新的邮件</a>
    </div>
  </article>
{/if}
