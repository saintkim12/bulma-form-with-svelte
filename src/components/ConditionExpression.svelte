<script>
  const TYPE = 'expression'
  export let item
  $: if (item && item.type === TYPE && typeof item.getExpression !== 'function') {
    // console.log('if (item)')
    item.getExpression = () => item.value
  }
  function onValueTypeChange() {
     item.value = ''
  }
</script>

<div class="control is-expanded">
  <input class="input is-fullwidth" type="text" bind:value={item.value} placeholder="Text input" />
</div>
