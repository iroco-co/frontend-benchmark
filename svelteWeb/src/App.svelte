<script lang="ts">
  import {Router, Link, Route} from "svelte-routing"
  import Landing from "./modules/Landing.svelte";
  export let url = ""
</script>

<Router url="{url}">
  <div>
    <Route path="/:mail" component="{Landing}" />
    <Route path="/"><Landing /></Route>
  </div>
</Router>
