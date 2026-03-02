<!--
@component
GroceryPriceCalculator.svelte — Interactive Grocery Price Tracker

Allows users to select grocery items and see the price increases mentioned in the article.

USAGE EXAMPLE:
<GroceryPriceCalculator />
-->
<script>
  let selectedItems = $state([]);

  const groceryItems = [
    { id: 'beef', name: 'Beef', priceChange: '+16.4%', oldPrice: 'was ~$8.50/lb' },
    { id: 'coffee', name: 'Coffee', priceChange: '+19.8%', oldPrice: 'was ~$5.00/lb' },
    { id: 'lettuce', name: 'Lettuce', priceChange: '+7.3%', oldPrice: 'was ~$2.00/head' },
    { id: 'fish', name: 'Frozen Fish', priceChange: '+8.6%', oldPrice: 'was ~$9.00/lb' },
    { id: 'groundbeef', name: 'Ground Beef', priceChange: '$6.69/lb', oldPrice: 'was $5.61/lb' },
    { id: 'bananas', name: 'Bananas', priceChange: '+5.9%', oldPrice: 'was ~$0.55/lb' },
    { id: 'eggs', name: 'Eggs', priceChange: '-20.9%', oldPrice: 'was ~$3.50/dz', discount: true },
  ];

  function toggleItem(id) {
    const index = selectedItems.indexOf(id);
    if (index > -1) {
      selectedItems.splice(index, 1);
    } else {
      selectedItems.push(id);
    }
    selectedItems = selectedItems;
  }

  function getItemCount() {
    return selectedItems.length;
  }
</script>

<div class="calculator">
  <h3>Which grocery items are affecting your budget?</h3>
  <p class="subtitle">Select the items you buy. See how much prices have changed.</p>

  <div class="items-list">
    {#each groceryItems as item (item.id)}
      <button 
        class="item"
        class:selected={selectedItems.includes(item.id)}
        onclick={() => toggleItem(item.id)}
      >
        <span class="checkbox">{selectedItems.includes(item.id) ? '✓' : '○'}</span>
        <div class="item-info">
          <span class="item-name">{item.name}</span>
          <span class="item-old-price">{item.oldPrice}</span>
        </div>
        <span class="item-change" class:discount={item.discount}>
          {item.priceChange}
        </span>
      </button>
    {/each}
  </div>

  {#if selectedItems.length > 0}
    <div class="summary">
      <p>You've selected <strong>{getItemCount()} item{getItemCount() !== 1 ? 's' : ''}</strong> that have increased in price.</p>
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
    cursor: pointer;
    width: 100%;
    text-align: left;
    transition: background-color 0.2s ease;

    &:last-child {
      border-bottom: none;
    }

    &:hover {
      background-color: rgba(0, 0, 0, 0.02);
    }

    &.selected {
      background-color: rgba(0, 81, 186, 0.05);
    }
  }

  .checkbox {
    font-size: 1.5rem;
    color: var(--color-medium-gray);
    flex-shrink: 0;
    width: 24px;
    text-align: center;

    .item.selected & {
      color: var(--color-link);
      font-weight: bold;
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

  .item-old-price {
    font-family: var(--font-sans);
    font-size: var(--font-size-xs);
    color: var(--color-medium-gray);
  }

  .item-change {
    font-family: var(--font-sans);
    font-weight: 600;
    color: #d32f2f;
    font-size: var(--font-size-sm);
    white-space: nowrap;
    padding: 0.25rem 0.5rem;
    background: rgba(211, 47, 47, 0.1);
    border-radius: 3px;

    &.discount {
      color: #388e3c;
      background: rgba(56, 142, 60, 0.1);
    }
  }

  .summary {
    padding: var(--spacing-sm);
    background: rgba(0, 81, 186, 0.08);
    border-left: 3px solid var(--color-link);
    margin-top: var(--spacing-md);

    p {
      margin: 0;
      font-size: var(--font-size-sm);
      color: var(--color-dark);
    }
  }
</style>
