<script>
  let roles = "ecuyer";
  import { TabGroup, Tab, TabAnchor } from "@skeletonlabs/skeleton";

  let tabSet = 0;
</script>

<TabGroup justify="justify-center">
  <Tab bind:group={tabSet} name="tab1" value={0}>
    <span>Jeu</span>
  </Tab>

  <Tab bind:group={tabSet} name="tab3" value={1}>Règle</Tab>
  <!-- Tab Panels --->

  <Tab bind:group={tabSet} name="tab3" value={2}>Avis</Tab>

  <svelte:fragment slot="panel">
    {#if tabSet === 0}
      <div>
        {#if (roles = "ecuyer")}
          <h1 class="h1">③① Ecuyer</h1>
          <p class="p">
            S'il est Dieu ou héro ou qu'uncun héros n'existe, le rôle n'est pas
            attribué et la personne boit.<br />

            L'écuyer boit à chaque fois que le héro boit.<br />

            Il perd son rôle si le héros perd son rôle.
          </p>
        {/if}
      </div>
    {:else if tabSet === 1}
      (tab panel 2 contents)
    {:else if tabSet === 2}
      (tab panel 3 contents)
    {/if}
  </svelte:fragment>
</TabGroup>
<p>mon glaive mon foie</p>
