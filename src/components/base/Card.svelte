<script lang="ts">
  export let title: string = "Card Title"
</script>

<div class={`${$$props.class}`}>
  <div class="bg-white rounded-md p-4">
    <h2 class="text-2xl text-center font-bold text-gray-900">{title}</h2>
    <slot />
  </div>
</div>
