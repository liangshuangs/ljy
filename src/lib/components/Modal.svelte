<script>
  import { createEventDispatcher } from 'svelte';
  
  export let show = false;
  export let title = '';
  export let size = 'medium';
  
  const dispatch = createEventDispatcher();
  
  function closeModal() {
    show = false;
    dispatch('close');
  }
  
  function handleBackdropClick(event) {
    if (event.target === event.currentTarget) {
      closeModal();
    }
  }
</script>

{#if show}
  <div class="modal-backdrop" on:click={handleBackdropClick} on:keydown>
    <div class="modal modal-{size}">
      <div class="modal-header">
        <h3 class="modal-title">{title}</h3>
        <button class="modal-close" on:click={closeModal}>×</button>
      </div>
      <div class="modal-body">
        <slot />
      </div>
      <div class="modal-footer">
        <slot name="footer" />
      </div>
    </div>
  </div>
{/if}

<style lang="less">
  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    animation: fadeIn 0.3s ease;
  }

  .modal {
    background: white;
    border-radius: 8px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    max-height: 90vh;
    overflow-y: auto;
    animation: slideIn 0.3s ease;

    &.modal-small {
      width: 400px;
      max-width: 90vw;
    }

    &.modal-medium {
      width: 600px;
      max-width: 90vw;
    }

    &.modal-large {
      width: 800px;
      max-width: 95vw;
    }
  }

  .modal-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1.5rem;
    border-bottom: 1px solid #e9ecef;

    .modal-title {
      margin: 0;
      font-size: 1.25rem;
      font-weight: 600;
      color: #343a40;
    }

    .modal-close {
      background: none;
      border: none;
      font-size: 2rem;
      line-height: 1;
      color: #6c757d;
      cursor: pointer;
      padding: 0;
      width: 2rem;
      height: 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 50%;
      transition: all 0.2s ease;

      &:hover {
        background-color: #f8f9fa;
        color: #495057;
      }
    }
  }

  .modal-body {
    padding: 1.5rem;
  }

  .modal-footer {
    padding: 1rem 1.5rem;
    border-top: 1px solid #e9ecef;
    display: flex;
    gap: 0.5rem;
    justify-content: flex-end;
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  @keyframes slideIn {
    from {
      opacity: 0;
      transform: scale(0.95) translateY(-10px);
    }
    to {
      opacity: 1;
      transform: scale(1) translateY(0);
    }
  }
</style>