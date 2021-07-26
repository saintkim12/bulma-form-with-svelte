<script>
  const TYPE = 'buy'
  export let item
  $: if (item && item.type === TYPE && typeof item.getExpression !== 'function') {
    // console.log('if (item)')
    item.getExpression = () => 'buy()'
  }
</script>

<div class="control is-expanded">
  <input class="input is-fullwidth" type="text" bind:value={item.value} placeholder="Text input" />
</div>
