<script>
  let roles = "hero";
  import { TabGroup, Tab, TabAnchor } from "@skeletonlabs/skeleton";
  import { Footer } from "flowbite-svelte";

  import ecu from "$lib/ecuyer.png";

  import dieu from "$lib/dieu.png";

  import mage from "$lib/mage.png";

  import hero from "$lib/hero.png";
  let tabSet = 0;

  let getDice = () => Math.floor(Math.random() * 6) + 1;
  let dice1 = getDice();
  let dice2 = getDice();
  let changeDices = () => {
    dice1 = getDice();
    dice2 = getDice();
    console.log(dice1, dice2);
    return null;
  };
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
      <div id="cards">
        <div class="card">
          <header class="card-header">
            <h2 class="h2">
              {dice1 > dice2 ? dice1 : dice2} - {dice2 < dice1 ? dice2 : dice1}
            </h2>
          </header>
          <section class="p-4">
            <br />
            <button
              type="button"
              on:click={changeDices}
              class="btn variant-filled"
            >
              Lancer les dés</button
            >
          </section>
        </div>

        {#if (roles === "ecuyer")}
          <div class="card">
            <header class="card-header">
              <div class="headercard">
                <img src={ecu} alt="ecuyer" />
              </div>
            </header>

            <section class="p-4">
              <p class="p">
                S'il est Dieu ou héro ou qu'uncun héros n'existe, le rôle n'est
                pas attribué et la personne boit.<br />

                L'écuyer boit à chaque fois que le héro boit.<br />

                Il perd son rôle si le héros perd son rôle.
              </p>
            </section>
            <footer class="card-footer"><h1 class="h1">③① Ecuyer</h1></footer>
          </div>

        {:else if (roles === "hero")}
          <div class="card">
            <header class="card-header">
              <div class="headercard">
                <img src={hero} alt="hero" />
              </div>
            </header>

            <section class="p-4">
              <p class="p">
                Quand le pouvoir du Dieu est déclenché (sur un total de 7 points
                sur un jet), une fois qu’il a distribué ses coups, le Héro est
                obligé de s’interposer. <br />
                Il lance alors un dé pour protéger les personnes visées.
                <br />
              </p>
            </section>
            <footer class="card-footer"><h1 class="h1">①① / ②② / ③③ Héro</h1></footer>
          </div>
        {/if}
      </div>

      AIDE DE JEU Dé 1 Dé 2 Action 1 1 Devient le héro, distribue 1 (Par
      tradition à l’ancien héro) 2 1 Devient Maître du destin 2 2 Devient le
      héro, distribue 2 (Par tradition à l’ancien héro) 3 1 Devient écuyer 3 2
      Rien : Boit 3 3 Devient le héro, Distribue 3 (Par tradition à l’ancien
      héro) 4 1 Rien : Boit 4 2 LAN au village, tout le monde boit 4 3 Dieu
      distribue 4, le héro s’interposeOURien : Boit 4 4 Devient Dieu (Duel),
      Distribue 4 (Par tradition à l’ancien dieu) 5 1 Fête au village : tout le
      monde boit 5 2 Dieu distribue 5, le héro s’interpose OU Rien : Boit 5 3
      Rien : Boit 5 4 Rien : Boit 5 5 Devient Dieu (Duel), Distribue 5 (Par
      tradition à l’ancien dieu) 6 1 Distribue 1 ET Dieu distribue 6, le héro
      s’interpose 6 2 Distribue 2 6 3 Distribue 3 6 4 Distribue 4 6 5 Distribue
      5 6 6 Devient Dieu, Distribue 6 (Par tradition à l’ancien dieu)
    {:else if tabSet === 1}
      <h1 class="h1">Mon foie est mon glaive</h1>
      <br />
      <br />
      <h2 class="h2">Dieu</h2>
      <br />

      <h3 class="h3">Devenir dieu</h3>
      <p>
        Ascension : en cas de double 4, 5 ou 6, il y a ascension et le joueur
        devient dieu. Il distribue alors la valeur de son double (4, 5 ou 6
        coups).<br />

        Duel de dieux : si le joueur fait un double 4 ou 5 et qu’un dieu est
        déjà en place, c’est un challenge, qui se résout sous la forme d’un
        duel: les deux joueurs lancent chacun un dé. Celui qui obtient le plus
        haut score devient alors dieu, le lanceur du plus bas boit 2 fois la
        différence. En cas d’égalité, le duel est renouvelé, et le perdant doit
        boire 3 fois la différence, et ainsi de suite.<br />

        Tradition : Les coups à distribuer pour les doubles se donnent par
        tradition à l’ancien dieu (ceci n’est pas une règle immuable).<br />
      </p>

      <br />
      <h3 class="h3">Le rôle de dieu</h3>
      <p>
        Au cas où le total des 2 dés fait 7, le dieu distribue le nombre de
        coups inscrit sur le dé le plus fort. (exemple : 43 = Dieu distribue 4)<br
        />
      </p>
      <br />
      <h3 class="h3">Perte du statut</h3>
      <p>Dieu perd son statut quand un autre dieu prend sa place.</p>
      <br />
      <h2 class="h2">Le héro</h2>

      <br />
      <h3 class="h3">Devenir le héro</h3>

      <p>
        Adoubement : En cas de double 1, 2, ou 3, le joueur devient le nouveau
        héro et distribue la valeur de son double (1 2 ou 3 coups)<br />

        Exceptions : Dieu ne pouvant être héro, si Dieu fait un score
        d’adoubement, il désigne un autre joueur qui deviendra héros à sa place.
        Les coups sont quand même distribués par le joueur qui a lancé les dés
        (ici, dieu).<br />

        Tradition : Les coups à distribuer pour les doubles se donnent par
        tradition à l’ancien héro (ceci n’est pas une règle immuable).<br />
      </p>
      <br />
      >
      <h3 class="h3">Le rôle du héro</h3>
      <p>
        Quand le pouvoir du Dieu est déclenché (sur un total de 7 points sur un
        jet), une fois qu’il a distribué ses coups, le Héro est obligé de
        s’interposer. Il lance alors un dé pour protéger les personnes visées.
        Les conséquences sont différentes suivant le résultat du jet:<br /><br
        />
        Combinaison Action<br />
        <br /> 1 Désintégration : Echec critique, le héro boit son verre cul sec
        et perd son statut.
        <br /> 2 / 3 Le héro rate son intervention : il boit le total des coups
        distribués par dieu ET les personnes visées boivent ce qui leur a été
        distribué.
        <br /> 4 / 5 Le héro se sacrifie avec succès pour sauver les innocents :
        il boit le total des coups distribués par dieu. Les personnes visées ne
        boivent pas.
        <br /> 6 Action héroique : Dieu boit le total des coups qu’il a distribué
        à la place de ses cibles.
      </p>
      <br />
      <h3 class="h3">Perte du statut</h3>
      <p>
        Le héro perd son statut à l’apparition d’un nouveau héro ou en cas de
        désintégration.
      </p>
      <br />

      <h2 class="h2">Le maître du destin</h2>
      <br />
      <h3 class="h3">Devenir maître du destin</h3>
      <p>Le joueur devient maître du destin en cas de 21.</p>
      <br />

      <h3 class="h3">Le rôle du maître du destin</h3>
      <p>
        Quand le héro s’interpose, le maître du destin peut appliquer -1 ou +1
        au dé du héro (ou laisser le résultat tel quel). Règles spéciale (Ajout
        optionnel) Maiar : Le maître du destin peut obtenir un pouvoir
        exceptionnel en faisant deux autres 21 avant d’être destitué. Si tel est
        le cas, il peut modifier (+1 ou -1) n’importe quel dé de la partie. (0
        sur le dé du héro) : Si le héro fait un 1 en s’interposant et que le
        maître du destin fait -1 sur ce dé, le héro doit boire un verre sec
        concocté par dieu. (7 sur le dé du héro) : Si le héro fait un 6 en
        s’interposant et que le maître du destin fait +1 sur ce dé, dieu boit un
        verre sec concocté par le héro.
      </p>
      <br />
      <h3 class="h3">Perte du statut</h3>
      <p>
        Le maître du destin perd son rôle quand un autre joueur prend sa place.
      </p>
      <br />
      <h2 class="h2">L’écuyer</h2>
      <br />
      <h3 class="h3">Devenir l’écuyer du héro</h3>

      <p>En cas de 31, le joueur devient écuyer.</p>
      <br />
      <h3 class="h3">Le rôle de l’écuyer</h3>

      <p>
        L’écuyer suis fidèlement son héros, et l’assiste dans toutes ses actions
        : Dès que le héros boit, l’écuyer boit la même quantité.
      </p>

      <br />
      <h3 class="h3">Perte du statut</h3>
      <p>L’écuyer perd son statut quand une autre personne fait 31.</p>
      <br />
      <h2 class="h2">Règles pour tous:</h2>
      <br />
      <h3 class="h3">6X</h3>

      <p>
        Si un dé est à 6 et un autre dé à X différent de 6, le joueur distribue
        X.
      </p>
      <br />
      <h3 class="h3">42, LAN au village</h3>
      <p>
        En cas de 42, tout le monde boit. Si 42 sort plusieurs fois d’affilé,
        tout le monde boit autant de fois que le 42 est sortie d’affilé.
      </p>
      <br />

      <h3 class="h3">51, fête au village</h3>

      <p>
        En cas de 51, tout le monde boit. Si 51 sort plusieurs fois d’affilé,
        tout le monde boit autant de fois que le 51 est sortie d’affilé.
      </p>
      <br />
      <h3 class="h3">Autres scores</h3>

      <p>
        Tout score ne faisant pas avancer l’histoire fait boire le joueur qui a
        lancé les dés (1).
      </p>
      <br />

      <h3 class="h3">Duel de paysans et Tournois</h3>

      <p>
        Si un score X (inutile) sort plusieurs fois d’affilé, chaque joueur
        concerné doit lancer un dé.<br />
        Le joueur au score le moins élevé boit Y fois la différence entre son score
        et celui le plus élevé (Y = nombre de joueurs dans le tournois - 1).<br
        />
        Il est alors éliminé du tournoi et les joueurs continuent sans lui jusqu’à
        ce qu’il n’y en ait plus qu’un.<br />
        Egalités : En cas d’égalitée au score le plus bas, un duel s’effectue entre
        les scores les plus bas et y=y+1.<br />
      </p>
    {:else if tabSet === 2}
      En cours de developpement
    {/if}
  </svelte:fragment>
</TabGroup>
<a href="https://github.com/EmPierrain/MGMF/">github</a>

<style>
  #cards {
    display: block;
  }

  .card-header {
    justify-content: center;
  }

  .card {
    display: flex;
    align-items: center;
    justify-content: center;
    align-content: center;
  }

  .headercard {
    width: 100%;
    height: 100%;
  }
</style>
