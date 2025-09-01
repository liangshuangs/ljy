<script>
  import '../app.less';
  import Header from '$lib/components/Header.svelte';
  
  // 用户数据，实际应用中可以从状态管理或API获取
  let userName = '小明同学';
  let userAvatar = '👦';
  let studyTime = 25; // 今日已学习时间（分钟）
</script>

<div class="app">
  <Header 
    {userName} 
    {userAvatar} 
    bind:studyTime
  />

  <main>
    <slot />
  </main>

  <footer class="kids-footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-icon">🎓</div>
        <p>每天进步一点点，你就是最棒的小学霸！</p>
        <div class="footer-decoration">
          <span>⭐</span><span>🌟</span><span>✨</span>
        </div>
      </div>
    </div>
  </footer>
</div>

<style lang="less">
  .app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  main {
    flex: 1;
    padding: 0;
  }

  .kids-footer {
    background: linear-gradient(90deg, #a8edea, #fed6e3);
    color: #333;
    text-align: center;
    padding: 2rem 0;

    .footer-content {
      .footer-icon {
        font-size: 3rem;
        margin-bottom: 1rem;
        animation: bounce 2s ease-in-out infinite;
      }

      p {
        font-size: 1.2rem;
        font-weight: 600;
        margin-bottom: 1rem;
        color: #555;
      }

      .footer-decoration {
        display: flex;
        justify-content: center;
        gap: 1rem;
        font-size: 1.5rem;

        span {
          animation: twinkle 2s ease-in-out infinite;
          
          &:nth-child(2) {
            animation-delay: 0.5s;
          }
          
          &:nth-child(3) {
            animation-delay: 1s;
          }
        }
      }
    }
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-10px);
    }
    60% {
      transform: translateY(-5px);
    }
  }

  @keyframes twinkle {
    0%, 100% {
      transform: scale(1);
      opacity: 1;
    }
    50% {
      transform: scale(1.2);
      opacity: 0.7;
    }
  }

  @media (max-width: 768px) {
    .kids-footer {
      .footer-content p {
        font-size: 1rem;
      }
    }
  }
</style>