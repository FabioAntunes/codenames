<script>
  import { navigate } from "svelte-routing";
  import Layout from "../components/Layout.svelte";
  import Card from "../components/Card.svelte";
  import Button from "../components/Button.svelte";
  import generate from "../utils/generate";

  export let code;

  $: grid = code.slice(1);
  $: player = code[0] === "1" ? "blue" : "red";

  function handleClick() {
    const code = generate();
    navigate(`/${code}`);
  }
</script>

<style>
  .red {
    @apply text-red-500;
  }
  .blue {
    @apply text-blue-500;
  }
</style>

<Layout>
  <div class="flex-1 grid place-items-center place-self-center gap-4 w-80">
    <div>
      <p>
        use the map card to play the
        <a
          class="underline"
          target="_blank"
          href="https://en.wikipedia.org/wiki/Codenames_(board_game)">codenames</a>
        board game, the
        <span
          class:red={player === 'red'}
          class:blue={player === 'blue'}
          class="font-bold">{player}
          agents</span>
        start this round
      </p>
    </div>
    <Card {player} {grid} />
    <div>
      <Button onClick={handleClick}>recreate</Button>
    </div>
  </div>
</Layout>
