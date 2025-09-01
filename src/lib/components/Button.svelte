<script>
  export let variant = 'primary';
  export let size = 'medium';
  export let disabled = false;
  export let loading = false;
  
  $: buttonClass = `btn btn-${variant} btn-${size}`;
</script>

<button 
  class={buttonClass}
  class:loading
  {disabled}
  on:click
  {...$$restProps}
>
  {#if loading}
    <span class="spinner"></span>
  {/if}
  <slot />
</button>

<style lang="less">
  .btn {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    font-weight: 500;
    text-align: center;
    text-decoration: none;
    transition: all 0.2s ease-in-out;
    cursor: pointer;
    border: 1px solid transparent;

    &:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    &.loading {
      pointer-events: none;
    }

    // 尺寸变体
    &.btn-small {
      padding: 0.25rem 0.75rem;
      font-size: 0.875rem;
    }

    &.btn-medium {
      padding: 0.5rem 1rem;
      font-size: 1rem;
    }

    &.btn-large {
      padding: 0.75rem 1.5rem;
      font-size: 1.125rem;
    }

    // 颜色变体
    &.btn-primary {
      background-color: #007bff;
      border-color: #007bff;
      color: white;

      &:hover:not(:disabled) {
        background-color: #0056b3;
        border-color: #0056b3;
      }
    }

    &.btn-secondary {
      background-color: #6c757d;
      border-color: #6c757d;
      color: white;

      &:hover:not(:disabled) {
        background-color: #545b62;
        border-color: #545b62;
      }
    }

    &.btn-success {
      background-color: #28a745;
      border-color: #28a745;
      color: white;

      &:hover:not(:disabled) {
        background-color: #1e7e34;
        border-color: #1e7e34;
      }
    }

    &.btn-outline {
      background-color: transparent;
      color: #007bff;
      border-color: #007bff;

      &:hover:not(:disabled) {
        background-color: #007bff;
        color: white;
      }
    }
  }

  .spinner {
    width: 1em;
    height: 1em;
    border: 2px solid currentColor;
    border-top: 2px solid transparent;
    border-radius: 50%;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
</style>