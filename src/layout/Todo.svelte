<script lang="ts">
  import Card from "../components/base/Card.svelte";
  import Todos from "../components/Todos.svelte";
</script>

<main class={`${$$props.class}`}>
  <div class="h-screen grid place-items-center bg-gray-900">
    <div class="w-full max-w-screen-sm">
      <Card title="TODO App" class="p-2">
        <Todos class="my-2" />
      </Card>
    </div>
  </div>
</main>
