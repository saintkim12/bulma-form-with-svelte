<script>
  const TYPE = 'percent'
  const KEY = 'percent'
  export let item
  $: if (item && item.type === TYPE && typeof item.getExpression !== 'function') {
    // console.log('if (item)')
    item.getExpression = () => [KEY, item.operation, item.value].filter(v => v === 0 || !!v).join(' ')
  }
  function onValueTypeChange() {
     item.value = ''
  }
</script>

<div class="control">
  <div class="select">
    <select bind:value={item.valueType} on:change={onValueTypeChange}>
      <option value="" style="display: none;">값 유형</option>
      <option value="number">number</option>
      <option value="prop">prop</option>
      <!-- <option value="expression">expression</option> -->
    </select>
  </div>
</div>
<div class="control is-expanded">
  {#if ['number'].includes(item.valueType)}
  <input class="input" type="number" bind:value={item.value} placeholder="Number input" />
  <!-- {:else if ['expression'].includes(item.valueType)} -->
  <!-- <input class="input is-fullwidth" type="text" bind:value={item.value} placeholder="Text input" /> -->
  {:else}
  <input class="input" type="text" bind:value={item.value} placeholder="Text input" />
  {/if}
</div>
<!-- {#if ['expression'].includes(item.valueType)} -->
  <!--  -->
<!-- {:else} -->
<div class="control">
  <div class="select">
    <select bind:value={item.operation}>
      <option value="" style="display: none;">Select</option>
      <option value=">=">&gt;=</option>
      <option value="<=">&lt;=</option>
      <option value=">">&gt;</option>
      <option value="<">&lt;</option>
    </select>
  </div>
</div>
<!-- {/if} -->
