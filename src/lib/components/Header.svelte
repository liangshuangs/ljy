<script>
  import { onMount } from 'svelte';
  
  export let userName = '小明同学';
  export let userAvatar = '👦';
  export let studyTime = 0; // 学习时间（分钟）
  
  let currentTime = '';
  let studyTimer = null;
  let isStudying = false;
  
  // 更新当前时间
  function updateTime() {
    const now = new Date();
    const hours = now.getHours().toString().padStart(2, '0');
    const minutes = now.getMinutes().toString().padStart(2, '0');
    currentTime = `${hours}:${minutes}`;
  }
  
  // 开始/停止学习计时
  function toggleStudyTimer() {
    if (isStudying) {
      clearInterval(studyTimer);
      isStudying = false;
    } else {
      studyTimer = setInterval(() => {
        studyTime++;
      }, 60000); // 每分钟更新一次
      isStudying = true;
    }
  }
  
  // 格式化学习时间显示
  function formatStudyTime(minutes) {
    const hours = Math.floor(minutes / 60);
    const mins = minutes % 60;
    if (hours > 0) {
      return `${hours}小时${mins}分钟`;
    }
    return `${mins}分钟`;
  }
  
  onMount(() => {
    updateTime();
    const timeInterval = setInterval(updateTime, 1000);
    
    return () => {
      clearInterval(timeInterval);
      if (studyTimer) clearInterval(studyTimer);
    };
  });
</script>

<nav class="kids-navbar">
  <div class="container">
    <div class="nav-content">
      <!-- 品牌标识 -->
      <div class="nav-brand">
        <span class="brand-icon">🌈</span>
        <span class="brand-text">小学生学习乐园</span>
      </div>
      
      <!-- 中间区域 - 学习时间 -->
      <div class="nav-center">
        <div class="current-time">
          <span class="time-icon">🕐</span>
          <span class="time-text">{currentTime}</span>
        </div>
        
        <div class="study-timer">
          <button 
            class="timer-btn" 
            class:active={isStudying}
            on:click={toggleStudyTimer}
          >
            <span class="timer-icon">{isStudying ? '⏸️' : '▶️'}</span>
            <span class="timer-text">
              {isStudying ? '暂停学习' : '开始学习'}
            </span>
          </button>
          
          {#if studyTime > 0}
            <div class="study-time-display">
              <span class="study-icon">📚</span>
              <span>今日已学: {formatStudyTime(studyTime)}</span>
            </div>
          {/if}
        </div>
      </div>
      
      <!-- 右侧区域 - 用户信息 -->
      <div class="nav-user">
        <div class="user-info">
          <span class="user-avatar">{userAvatar}</span>
          <div class="user-details">
            <span class="user-name">{userName}</span>
            <div class="user-stats">
              <span class="stat-item">
                <span class="stat-icon">⭐</span>
                <span class="stat-value">85</span>
              </span>
              <span class="stat-item">
                <span class="stat-icon">🏆</span>
                <span class="stat-value">12</span>
              </span>
            </div>
          </div>
        </div>
        
        <div class="user-actions">
          <button class="action-btn settings">
            <span>⚙️</span>
          </button>
          <button class="action-btn logout">
            <span>👋</span>
          </button>
        </div>
      </div>
    </div>
    
    <!-- 学习进度条 -->
    {#if isStudying}
      <div class="study-progress">
        <div class="progress-bar">
          <div class="progress-fill" style="animation: studying 2s ease-in-out infinite;"></div>
        </div>
        <span class="progress-text">正在专心学习中... 🎯</span>
      </div>
    {/if}
  </div>
</nav>

<style lang="less">
  .kids-navbar {
    background: linear-gradient(135deg, #ff6b6b, #4ecdc4, #45b7d1, #a8edea);
    box-shadow: 0 4px 20px rgba(0,0,0,0.15);
    padding: 1rem 0;
    position: relative;
    overflow: hidden;

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
      animation: shine 3s ease-in-out infinite;
    }

    .nav-content {
      display: grid;
      grid-template-columns: auto 1fr auto;
      gap: 2rem;
      align-items: center;
    }

    .nav-brand {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      color: white;
      text-decoration: none;
      font-weight: bold;

      .brand-icon {
        font-size: 2.5rem;
        animation: rainbow 3s ease-in-out infinite;
        filter: drop-shadow(2px 2px 4px rgba(0,0,0,0.3));
      }

      .brand-text {
        font-size: 1.5rem;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        background: linear-gradient(45deg, #fff, #f0f8ff);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        font-weight: 800;
      }
    }

    .nav-center {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 2rem;

      .current-time {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        background: rgba(255,255,255,0.2);
        padding: 0.5rem 1rem;
        border-radius: 20px;
        color: white;
        font-weight: bold;
        backdrop-filter: blur(10px);

        .time-icon {
          font-size: 1.2rem;
          animation: tick 1s ease-in-out infinite;
        }

        .time-text {
          font-size: 1.1rem;
          font-family: 'Courier New', monospace;
        }
      }

      .study-timer {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 0.5rem;

        .timer-btn {
          display: flex;
          align-items: center;
          gap: 0.5rem;
          background: rgba(255,255,255,0.9);
          border: none;
          padding: 0.5rem 1rem;
          border-radius: 25px;
          cursor: pointer;
          transition: all 0.3s ease;
          font-weight: bold;
          color: #333;

          &:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
          }

          &.active {
            background: #4caf50;
            color: white;
            animation: pulse 1.5s ease-in-out infinite;
          }

          .timer-icon {
            font-size: 1.1rem;
          }
        }

        .study-time-display {
          display: flex;
          align-items: center;
          gap: 0.3rem;
          background: rgba(76, 175, 80, 0.9);
          color: white;
          padding: 0.3rem 0.8rem;
          border-radius: 15px;
          font-size: 0.9rem;
          font-weight: bold;
          animation: glow 2s ease-in-out infinite;

          .study-icon {
            animation: float 2s ease-in-out infinite;
          }
        }
      }
    }

    .nav-user {
      display: flex;
      align-items: center;
      gap: 1rem;

      .user-info {
        display: flex;
        align-items: center;
        gap: 0.8rem;
        background: rgba(255,255,255,0.15);
        padding: 0.8rem;
        border-radius: 20px;
        backdrop-filter: blur(10px);

        .user-avatar {
          font-size: 2rem;
          animation: bounce 2s ease-in-out infinite;
        }

        .user-details {
          .user-name {
            display: block;
            color: white;
            font-weight: bold;
            font-size: 1rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
          }

          .user-stats {
            display: flex;
            gap: 0.8rem;
            margin-top: 0.2rem;

            .stat-item {
              display: flex;
              align-items: center;
              gap: 0.2rem;
              font-size: 0.8rem;
              color: rgba(255,255,255,0.9);

              .stat-icon {
                font-size: 0.9rem;
              }
            }
          }
        }
      }

      .user-actions {
        display: flex;
        gap: 0.5rem;

        .action-btn {
          background: rgba(255,255,255,0.2);
          border: none;
          width: 40px;
          height: 40px;
          border-radius: 50%;
          cursor: pointer;
          transition: all 0.3s ease;
          backdrop-filter: blur(10px);

          &:hover {
            background: rgba(255,255,255,0.3);
            transform: scale(1.1);
          }

          span {
            font-size: 1.2rem;
          }
        }
      }
    }

    .study-progress {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      background: rgba(0,0,0,0.1);
      padding: 0.5rem 1rem;
      display: flex;
      align-items: center;
      gap: 1rem;

      .progress-bar {
        flex: 1;
        height: 6px;
        background: rgba(255,255,255,0.3);
        border-radius: 3px;
        overflow: hidden;

        .progress-fill {
          height: 100%;
          background: linear-gradient(90deg, #4caf50, #8bc34a);
          border-radius: 3px;
        }
      }

      .progress-text {
        color: white;
        font-size: 0.9rem;
        font-weight: bold;
        text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
      }
    }
  }

  @keyframes rainbow {
    0%, 100% { transform: rotate(0deg); }
    25% { transform: rotate(-10deg); }
    75% { transform: rotate(10deg); }
  }

  @keyframes shine {
    0% { left: -100%; }
    100% { left: 100%; }
  }

  @keyframes tick {
    0%, 50%, 100% { transform: scale(1); }
    25%, 75% { transform: scale(1.1); }
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.05); }
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
    40% { transform: translateY(-8px); }
    60% { transform: translateY(-4px); }
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-3px); }
  }

  @keyframes glow {
    0%, 100% { box-shadow: 0 0 5px rgba(76, 175, 80, 0.5); }
    50% { box-shadow: 0 0 15px rgba(76, 175, 80, 0.8); }
  }

  @keyframes studying {
    0% { width: 0%; }
    50% { width: 70%; }
    100% { width: 100%; }
  }

  @media (max-width: 1024px) {
    .kids-navbar {
      .nav-content {
        grid-template-columns: 1fr;
        gap: 1rem;
        text-align: center;
      }

      .nav-center {
        order: 2;
        flex-direction: column;
        gap: 1rem;
      }

      .nav-user {
        order: 3;
        justify-content: center;
      }
    }
  }

  @media (max-width: 768px) {
    .kids-navbar {
      .nav-brand .brand-text {
        font-size: 1.2rem;
      }

      .nav-center {
        .current-time, .timer-btn {
          font-size: 0.9rem;
          padding: 0.4rem 0.8rem;
        }
      }

      .nav-user .user-info {
        padding: 0.6rem;
        
        .user-details .user-name {
          font-size: 0.9rem;
        }
      }
    }
  }
</style>