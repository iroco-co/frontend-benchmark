<script lang="ts">
    import { onMount } from 'svelte'
    import { navigate } from 'svelte-routing'

    import Viewer from './MailViewer.svelte'
    import { fetchMails } from "./mails/api.js"
    import MailList from "./MailList.svelte"
    import Header from "./Header.svelte"

    let mails = []
    let selectedMailId = null

    onMount(async () => {
        mails = await fetchMails()
        if (mails.length) {
            selectedMailId = mails[0].id
            navigate(`/${selectedMailId}`)
        }
    })
</script>

<Header/>

<div class="mails-landing">
    <div class="list">
      <MailList mails={mails} bind:selectedMailId/>
    </div>

    {#if selectedMailId !== null}
        <div class="viewer">
          <Viewer selectedMailId={selectedMailId} />
        </div>
    {/if}
</div>

<style lang="scss">
  .mails-landing {
    width: 100%;
    height: calc(100% - 80px);
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;

    >.list {
      width: 300px;
      height: 100%;
    }

    >.viewer {
      width: calc(100% - 300px);
      height: 100%;
      border-left: solid $light-grey 1px;
    }
  }
</style>