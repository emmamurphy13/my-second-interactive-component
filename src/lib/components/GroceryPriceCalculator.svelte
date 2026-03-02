<!--
@component
GroceryPriceCalculator.svelte — Interactive Grocery Price Tracker

Allows users to select grocery items, input quantities, and calculate total costs.

USAGE EXAMPLE:
<GroceryPriceCalculator />
-->
<script>
  let quantities = $state({});

  const groceryItems = [
    { id: 'beef', name: 'Beef', currentPrice: 9.89, oldPrice: 8.50, unit: '/lb', discount: false },
    { id: 'coffee', name: 'Coffee', currentPrice: 5.99, oldPrice: 5.00, unit: '/lb', discount: false },
    { id: 'lettuce', name: 'Lettuce', currentPrice: 2.15, oldPrice: 2.00, unit: '/head', discount: false },
    { id: 'fish', name: 'Frozen Fish', currentPrice: 9.77, oldPrice: 9.00, unit: '/lb', discount: false },
    { id: 'groundbeef', name: 'Ground Beef', currentPrice: 6.69, oldPrice: 5.61, unit: '/lb', discount: false },
    { id: 'bananas', name: 'Bananas', currentPrice: 0.58, oldPrice: 0.55, unit: '/lb', discount: false },
    { id: 'eggs', name: 'Eggs', currentPrice: 2.77, oldPrice: 3.50, unit: '/dz', discount: true },
  ];

  function calculateTotal() {
    let total = 0;
    for (const id in quantities) {
      const quantity = parseFloat(quantities[id]) || 0;
      const item = groceryItems.find(i => i.id === id);
      if (item && quantity > 0) {
        total += item.currentPrice * quantity;
      }
    }
    return total.toFixed(2);
  }

  function calculateOldTotal() {
    let total = 0;
    for (const id in quantities) {
      const quantity = parseFloat(quantities[id]) || 0;
      const item = groceryItems.find(i => i.id === id);
      if (item && quantity > 0) {
        total += item.oldPrice * quantity;
      }
    }
    return total.toFixed(2);
  }

  function getSelectedCount() {
    return Object.keys(quantities).filter(id => parseFloat(quantities[id]) > 0).length;
  }

  function hasQuantities() {
    return Object.values(quantities).some(q => parseFloat(q) > 0);
  }
</script>

<div class="calculator">
  <h3>Calculate your grocery bill</h3>
  <p class="subtitle">Enter quantities to see how much prices have increased</p>

  <div class="items-list">
    {#each groceryItems as item (item.id)}
      <div class="item">
        <div class="item-info">
          <span class="item-name">{item.name}</span>
          <span class="item-price" class:discount={item.discount}>
            ${item.currentPrice.toFixed(2)}{item.unit}
            {#if !item.discount}
              <span class="price-change">(was ${item.oldPrice.toFixed(2)}{item.unit})</span>
            {:else}
              <span class="price-change discount-text">(was ${item.oldPrice.toFixed(2)}{item.unit})</span>
            {/if}
          </span>
        </div>
        <div class="item-input">
          <input 
            type="number" 
            placeholder="0" 
            min="0" 
            step="0.1"
            bind:value={quantities[item.id]}
            class="quantity-input"
          />
          <span class="unit-label">{item.unit.substring(1)}</span>
        </div>
      </div>
    {/each}
  </div>

  {#if hasQuantities()}
    <div class="summary">
      <div class="summary-row">
        <span class="summary-label">You selected:</span>
        <span class="summary-value">{getSelectedCount()} item{getSelectedCount() !== 1 ? 's' : ''}</span>
      </div>
      <div class="summary-row">
        <span class="summary-label">Current total cost:</span>
        <span class="summary-value current">${calculateTotal()}</span>
      </div>
      <div class="summary-row">
        <span class="summary-label">Previous total cost:</span>
        <span class="summary-value old">${calculateOldTotal()}</span>
      </div>
      <div class="summary-row difference">
        <span class="summary-label">Price increase:</span>
        <span class="summary-value increase">+${(calculateTotal() - calculateOldTotal()).toFixed(2)}</span>
      </div>
    </div>
  {/if}
</div>

<style lang="scss">
  @use '../styles' as *;

  .calculator {
    padding: var(--spacing-md);
    background: var(--color-light-gray);
    margin: var(--spacing-lg) 0;
    border-left: 4px solid var(--color-dark);
  }

  h3 {
    margin: 0 0 var(--spacing-xs) 0 !important;
    font-family: var(--font-serif);
    font-size: var(--font-size-lg);
    font-weight: 600;
    color: var(--color-dark);
  }

  .subtitle {
    margin: 0 0 var(--spacing-md) 0;
    font-size: var(--font-size-sm);
    color: var(--color-medium-gray);
  }

  .items-list {
    display: flex;
    flex-direction: column;
    gap: 0;
    margin-bottom: var(--spacing-md);
  }

  .item {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    padding: var(--spacing-sm);
    border: none;
    border-bottom: 1px solid var(--color-border);
    background: transparent;
    width: 100%;
    text-align: left;
    transition: background-color 0.2s ease;

    &:last-child {
      border-bottom: none;
    }

    &:hover {
      background-color: rgba(0, 0, 0, 0.02);
    }
  }

  .item-info {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    flex: 1;
  }

  .item-name {
    font-family: var(--font-sans);
    font-weight: 500;
    color: var(--color-dark);
    font-size: var(--font-size-base);
  }

  .item-price {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    color: var(--color-dark);
    font-weight: 600;

    &.discount {
      color: #388e3c;
    }
  }

  .price-change {
    font-weight: 400;
    color: var(--color-medium-gray);
    display: block;
    font-size: var(--font-size-xs);
    margin-top: 0.25rem;

    &.discount-text {
      color: #388e3c;
    }
  }

  .item-input {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-shrink: 0;
  }

  .quantity-input {
    width: 70px;
    padding: 0.5rem;
    border: 1px solid var(--color-border);
    border-radius: 3px;
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    text-align: center;

    &:focus {
      outline: none;
      border-color: var(--color-link);
      box-shadow: 0 0 0 2px rgba(0, 81, 186, 0.1);
    }
  }

  .unit-label {
    font-family: var(--font-sans);
    font-size: var(--font-size-xs);
    color: var(--color-medium-gray);
    min-width: 35px;
    text-align: left;
  }

  .summary {
    padding: var(--spacing-md);
    background: rgba(0, 81, 186, 0.08);
    border: 1px solid rgba(0, 81, 186, 0.2);
    border-radius: 3px;
    margin-top: var(--spacing-md);
  }

  .summary-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem 0;
    border-bottom: 1px solid rgba(0, 81, 186, 0.1);

    &:last-child {
      border-bottom: none;
    }

    &.difference {
      padding-top: var(--spacing-sm);
      margin-top: var(--spacing-sm);
      border-top: 2px solid rgba(0, 81, 186, 0.2);
    }
  }

  .summary-label {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    color: var(--color-dark);
    font-weight: 500;
  }

  .summary-value {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 600;
    color: var(--color-dark);

    &.current {
      color: var(--color-dark);
    }

    &.old {
      color: var(--color-medium-gray);
    }

    &.increase {
      color: #d32f2f;
      font-size: var(--font-size-lg);
    }
  }
</style>
