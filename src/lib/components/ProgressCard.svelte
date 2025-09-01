<script>
  export let subject = '';
  export let progress = 0;
  
  const maxStars = 5;
  $: filledStars = Math.floor((progress / 100) * maxStars);
  $: emptyStars = maxStars - filledStars;
</script>

<div class="progress-card">
  <div class="progress-header">
    <h3>{subject} 学习进度</h3>
    <div class="stars">
      {#each Array(filledStars) as _}
        <span class="star filled">⭐</span>
      {/each}
      {#each Array(emptyStars) as _}
        <span class="star empty">☆</span>
      {/each}
    </div>
  </div>
  
  <div class="progress-bar">
    <div class="progress-fill" style="width: {progress}%"></div>
  </div>
  
  <div class="progress-text">
    <span>完成度: {progress}%</span>
    <span class="progress-level">
      {#if progress < 20}
        🌱 萌芽期
      {:else if progress < 40}
        🌿 成长期  
      {:else if progress < 60}
        🌸 开花期
      {:else if progress < 80}
        🌺 盛开期
      {:else}
        🏆 学霸期
      {/if}
    </span>
  </div>
</div>

<style lang="less">
  .progress-card {
    background: linear-gradient(135deg, #fff8e1, #fff3e0);
    border-radius: 15px;
    padding: 1.5rem;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    border: 2px solid #ffd54f;
    margin-bottom: 1rem;
  }

  .progress-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;

    h3 {
      font-size: 1.2rem;
      color: #e65100;
      margin: 0;
    }

    .stars {
      display: flex;
      gap: 0.2rem;

      .star {
        font-size: 1.5rem;
        transition: all 0.3s ease;

        &.filled {
          animation: sparkle 2s ease-in-out infinite;
        }

        &.empty {
          opacity: 0.3;
        }
      }
    }
  }

  .progress-bar {
    background: #fff;
    border-radius: 10px;
    height: 12px;
    overflow: hidden;
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
    margin-bottom: 1rem;

    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #4caf50, #8bc34a);
      border-radius: 10px;
      transition: width 0.8s ease;
      position: relative;

      &::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(
          90deg,
          transparent,
          rgba(255,255,255,0.3),
          transparent
        );
        animation: shimmer 2s ease-in-out infinite;
      }
    }
  }

  .progress-text {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 0.9rem;
    color: #bf360c;
    font-weight: 600;

    .progress-level {
      font-size: 1rem;
      background: #fff;
      padding: 0.2rem 0.8rem;
      border-radius: 15px;
      border: 1px solid #ffcc02;
    }
  }

  @keyframes sparkle {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
  }

  @keyframes shimmer {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(100%); }
  }
</style>