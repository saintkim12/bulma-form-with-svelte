<!-- src/components/RequestsForm.svelte -->
<script>
import ConditionPercent from './ConditionPercent.svelte'
import ConditionExpression from './ConditionExpression.svelte'
import ActionBuy from './ActionBuy.svelte'

  $: formData = {
    requests: [
      { condition: `percent > 100`, action: 'allIn()' },
      { condition: 'cc', action: 'dd' },
    ],
  }
  $: uiData = {
    requests: [
      { condition: { type: '' }, action: { type: '' } },
      { condition: { type: '' }, action: { type: '' } },
    ],
  }
</script>

<div ref="requestsForm" class="columns">
  <div class="column is-half">
    <pre>
      {JSON.stringify(formData, null, 2)}
    </pre>
    <pre>
      {JSON.stringify(uiData, null, 2)}
    </pre>
  </div>
  <div class="column is-half">
    <div class="field">
      <span class="label">Name</span>
      <div class="control">
        <input class="input" type="text" placeholder="Text input" />
      </div>
    </div>
    <hr />
    {#each formData.requests as { condition, action }, i}
      <div class="field">
        <span class="label">Condition {i + 1}</span>
      </div>
      <div class="field has-addons">
        <div class="control">
          <div class="select">
            <select bind:value={uiData.requests[i].condition.type}>
              <option value="" style="display: none;">Select</option>
              <option value="percent">percent</option>
              <option value="expression">expression</option>
            </select>
          </div>
        </div>
        {#if !uiData.requests[i].condition.type}
        <div class="control is-expanded">
          <input class="input is-fullwidth" type="text" placeholder="Text input" />
        </div>
        {:else if uiData.requests[i].condition.type === 'percent'}
        <ConditionPercent bind:item={uiData.requests[i].condition} />
        {:else if uiData.requests[i].condition.type === 'expression'}
        <ConditionExpression bind:item={uiData.requests[i].condition} />
        {:else}
        <div class="control is-expanded">
          <input class="input is-fullwidth" type="text" placeholder="Text input" />
        </div>
        {/if}
        <div class="control">
          <button type="submit" class="button is-primary" on:click={e => {
            const data = uiData.requests[i].condition
            if (['percent', 'expression'].includes(data.type)) {
              formData.requests[i].condition = data.getExpression()
              uiData.requests[i].condition = { type: '' }
            }
          }}>Input</button>
        </div>
      </div>
      <div class="field">
        <textarea class="textarea" type="text" rows="3" placeholder="Text input" bind:value={condition} />
      </div>
      <div class="field">
        <span class="label">Action {i + 1}</span>
      </div>
      <div class="field has-addons">
        <div class="control">
          <div class="select">
            <select bind:value={uiData.requests[i].action.type}>
              <option value="" style="display: none;">Select</option>
              <option value="buy">buy</option>
              <option value="expression">expression</option>
            </select>
          </div>
        </div>
        {#if !uiData.requests[i].action.type}
        <div class="control is-expanded">
          <input class="input is-fullwidth" type="text" placeholder="Text input" />
        </div>
        {:else if uiData.requests[i].action.type === 'buy'}
        <ActionBuy bind:item={uiData.requests[i].action} />
        {:else}
        <div class="control is-expanded">
          <input class="input is-fullwidth" type="text" placeholder="Text input" />
        </div>
        {/if}
        <div class="control">
          <button type="submit" class="button is-primary" on:click={e => {
            const data = uiData.requests[i].action
            if (['buy'].includes(data.type)) {
              formData.requests[i].action = data.getExpression()
              uiData.requests[i].action = { type: '' }
            }
          }}>Input</button>
        </div>
      </div>
      <div class="field">
        <textarea class="textarea" type="text" rows="3" placeholder="Text input" bind:value={action} />
      </div>
    {/each}
    <hr />
    <div class="field">
      <span class="label">UserName</span>
      <div class="control has-icons-left has-icons-right">
        <input class="input is-success" type="text" placeholder="Text input" value="bulma" />
        <span class="icon is-small is-left">
          <i class="fas fa-user" />
        </span>
        <span class="icon is-small is-right">
          <i class="fas fa-check" />
        </span>
      </div>
      <p class="help is-success">This username is available</p>
    </div>

    <div class="field">
      <span class="label">Email</span>
      <div class="control has-icons-left has-icons-right">
        <input class="input is-danger" type="email" placeholder="Email input" value="hello@" />
        <span class="icon is-small is-left">
          <i class="fas fa-envelope" />
        </span>
        <span class="icon is-small is-right">
          <i class="fas fa-exclamation-triangle" />
        </span>
      </div>
      <p class="help is-danger">This email is invalid</p>
    </div>

    <div class="field">
      <span class="label">Subject</span>
      <div class="control">
        <div class="select">
          <select>
            <option>Select dropdown</option>
            <option>With options</option>
          </select>
        </div>
      </div>
    </div>

    <div class="field">
      <span class="label">Message</span>
      <div class="control">
        <textarea class="textarea" placeholder="Textarea" />
      </div>
    </div>

    <div class="field">
      <div class="control">
        <label class="checkbox">
          <input type="checkbox" />
          I agree to the <a href="#">terms and conditions</a>
        </label>
      </div>
    </div>

    <div class="field">
      <div class="control">
        <label class="radio">
          <input type="radio" name="question" />
          Yes
        </label>
        <label class="radio">
          <input type="radio" name="question" />
          No
        </label>
      </div>
    </div>

    <div class="field is-grouped">
      <div class="control">
        <button class="button is-link">Submit</button>
      </div>
      <div class="control">
        <button class="button is-link is-light">Cancel</button>
      </div>
    </div>
  </div>
</div>

<style lang="scss">
  :global(input[type=number]) {
    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }
    & {
      -moz-appearance: textfield;
    }
  }
</style>
