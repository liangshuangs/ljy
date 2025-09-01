<script>
  import { onMount } from 'svelte';
  
  let currentSubject = 'home';
  let isVisible = false;

  onMount(() => {
    isVisible = true;
  });

  function selectSubject(subject) {
    currentSubject = subject;
  }

  // 学科数据
  const subjects = {
    math: {
      name: '数学',
      icon: '🔢',
      color: '#ff6b6b',
      description: '和数字做朋友，学习有趣的数学知识！'
    },
    english: {
      name: '英语',
      icon: '🔤',
      color: '#4ecdc4', 
      description: '学习英语字母和单词，和世界交朋友！'
    },
    chinese: {
      name: '语文',
      icon: '📖',
      color: '#45b7d1',
      description: '读故事、写汉字，感受中文的美丽！'
    }
  };
</script>

<svelte:head>
  <title>小学生学习乐园</title>
  <meta name="description" content="适合小学生的在线学习平台，包含数学、英语、语文三个学科" />
</svelte:head>

<div class="learning-container">
  {#if currentSubject === 'home'}
    <!-- 主页 - 学科选择 -->
    <section class="welcome-section" class:visible={isVisible}>
      <div class="welcome-header">
        <h1 class="welcome-title">🌟 欢迎来到学习乐园 🌟</h1>
        <p class="welcome-subtitle">选择你想学习的学科，开始有趣的学习之旅吧！</p>
      </div>

      <div class="subjects-grid">
        {#each Object.entries(subjects) as [key, subject]}
          <div 
            class="subject-card" 
            style="--subject-color: {subject.color}"
            on:click={() => selectSubject(key)}
            on:keydown={(e) => e.key === 'Enter' && selectSubject(key)}
            tabindex="0"
            role="button"
          >
            <div class="subject-icon">{subject.icon}</div>
            <h3 class="subject-name">{subject.name}</h3>
            <p class="subject-description">{subject.description}</p>
            <div class="subject-button">开始学习</div>
          </div>
        {/each}
      </div>

      <div class="fun-facts">
        <h2 class="facts-title">🎯 学习小贴士</h2>
        <div class="facts-grid">
          <div class="fact-item">
            <span class="fact-icon">🎈</span>
            <p>每天学习30分钟，坚持就有大进步！</p>
          </div>
          <div class="fact-item">
            <span class="fact-icon">⭐</span>
            <p>做错题目不要紧，重要的是要思考为什么！</p>
          </div>
          <div class="fact-item">
            <span class="fact-icon">🏆</span>
            <p>完成练习题可以获得小星星奖励哦！</p>
          </div>
        </div>
      </div>
    </section>
  {:else}
    <!-- 学科学习页面 -->
    <section class="subject-learning">
      <div class="subject-header">
        <button class="back-button" on:click={() => selectSubject('home')}>
          ← 返回主页
        </button>
        <div class="subject-title" style="--subject-color: {subjects[currentSubject].color}">
          <span class="subject-icon-large">{subjects[currentSubject].icon}</span>
          <h1>{subjects[currentSubject].name}学习</h1>
        </div>
      </div>

      <div class="learning-content">
        {#if currentSubject === 'math'}
          <div class="math-content">
            <h2>🔢 数学乐园</h2>
            <div class="learning-modules">
              <div class="module-card">
                <h3>➕ 加法练习</h3>
                <p>学习数字相加，从简单的1+1开始！</p>
                <div class="example">例：2 + 3 = ?</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>➖ 减法练习</h3>
                <p>学习数字相减，理解减少的概念！</p>
                <div class="example">例：5 - 2 = ?</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>🔢 数数游戏</h3>
                <p>从1数到100，建立数字概念！</p>
                <div class="example">1, 2, 3, 4, 5...</div>
                <button class="practice-btn">开始练习</button>
              </div>
            </div>
          </div>
        {:else if currentSubject === 'english'}
          <div class="english-content">
            <h2>🔤 英语天地</h2>
            <div class="learning-modules">
              <div class="module-card">
                <h3>🔤 字母学习</h3>
                <p>学习26个英文字母的读音和写法！</p>
                <div class="example">A, B, C, D, E...</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>🍎 单词乐园</h3>
                <p>学习常用的英语单词，从苹果开始！</p>
                <div class="example">Apple 🍎 Cat 🐱 Dog 🐶</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>🎵 英语儿歌</h3>
                <p>通过唱歌学英语，更有趣更好记！</p>
                <div class="example">♪ ABC Song ♪</div>
                <button class="practice-btn">开始练习</button>
              </div>
            </div>
          </div>
        {:else if currentSubject === 'chinese'}
          <div class="chinese-content">
            <h2>📖 语文花园</h2>
            <div class="learning-modules">
              <div class="module-card">
                <h3>✏️ 汉字练习</h3>
                <p>学习常用汉字的笔画和部首！</p>
                <div class="example">一 二 三 四 五</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>📚 拼音乐园</h3>
                <p>学习拼音声母韵母，为阅读打基础！</p>
                <div class="example">a o e i u ü</div>
                <button class="practice-btn">开始练习</button>
              </div>
              <div class="module-card">
                <h3>🐰 故事阅读</h3>
                <p>读有趣的小故事，提高阅读能力！</p>
                <div class="example">🐰 小兔子的故事</div>
                <button class="practice-btn">开始练习</button>
              </div>
            </div>
          </div>
        {/if}
      </div>
    </section>
  {/if}
</div>

<style lang="less">
  @import '../app.less';

  // 专门为小学生设计的色彩变量
  @kids-red: #ff6b6b;
  @kids-blue: #45b7d1;
  @kids-green: #4ecdc4;
  @kids-yellow: #feca57;
  @kids-purple: #a55eea;
  @kids-orange: #ff9ff3;

  .learning-container {
    min-height: 100vh;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 2rem 0;
  }

  .welcome-section {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1rem;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease;

    &.visible {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .welcome-header {
    text-align: center;
    margin-bottom: 3rem;

    .welcome-title {
      font-size: 3rem;
      color: white;
      margin-bottom: 1rem;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
      animation: bounce 2s ease-in-out infinite;
    }

    .welcome-subtitle {
      font-size: 1.3rem;
      color: rgba(255,255,255,0.9);
      margin-bottom: 2rem;
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

  .subjects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }

  .subject-card {
    background: white;
    border-radius: 20px;
    padding: 2rem;
    text-align: center;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2);
    transition: all 0.3s ease;
    cursor: pointer;
    border: 4px solid var(--subject-color);
    position: relative;
    overflow: hidden;

    &:hover {
      transform: translateY(-10px) scale(1.02);
      box-shadow: 0 20px 40px rgba(0,0,0,0.3);
    }

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 8px;
      background: var(--subject-color);
    }

    .subject-icon {
      font-size: 4rem;
      margin-bottom: 1rem;
      animation: wiggle 2s ease-in-out infinite;
    }

    .subject-name {
      font-size: 2rem;
      font-weight: bold;
      color: var(--subject-color);
      margin-bottom: 1rem;
    }

    .subject-description {
      font-size: 1.1rem;
      color: #666;
      margin-bottom: 1.5rem;
      line-height: 1.6;
    }

    .subject-button {
      background: var(--subject-color);
      color: white;
      padding: 0.8rem 2rem;
      border-radius: 25px;
      font-weight: bold;
      font-size: 1.1rem;
      display: inline-block;
      transition: all 0.3s ease;

      &:hover {
        transform: scale(1.1);
        box-shadow: 0 5px 15px rgba(0,0,0,0.3);
      }
    }
  }

  @keyframes wiggle {
    0%, 7% {
      transform: rotateZ(0);
    }
    15% {
      transform: rotateZ(-15deg);
    }
    20% {
      transform: rotateZ(10deg);
    }
    25% {
      transform: rotateZ(-10deg);
    }
    30% {
      transform: rotateZ(6deg);
    }
    35% {
      transform: rotateZ(-4deg);
    }
    40%, 100% {
      transform: rotateZ(0);
    }
  }

  .fun-facts {
    background: white;
    border-radius: 20px;
    padding: 2rem;
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);

    .facts-title {
      text-align: center;
      font-size: 2rem;
      color: #333;
      margin-bottom: 2rem;
    }

    .facts-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
    }

    .fact-item {
      display: flex;
      align-items: center;
      gap: 1rem;
      padding: 1rem;
      background: #f8f9fa;
      border-radius: 15px;
      border-left: 4px solid @kids-yellow;

      .fact-icon {
        font-size: 2rem;
      }

      p {
        margin: 0;
        font-size: 1rem;
        color: #555;
        line-height: 1.5;
      }
    }
  }

  .subject-learning {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  .subject-header {
    display: flex;
    align-items: center;
    gap: 2rem;
    margin-bottom: 3rem;

    .back-button {
      background: white;
      border: none;
      padding: 0.8rem 1.5rem;
      border-radius: 25px;
      font-size: 1rem;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      transition: all 0.3s ease;

      &:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(0,0,0,0.2);
      }
    }

    .subject-title {
      display: flex;
      align-items: center;
      gap: 1rem;
      color: white;

      .subject-icon-large {
        font-size: 4rem;
        animation: pulse 2s ease-in-out infinite;
      }

      h1 {
        font-size: 3rem;
        margin: 0;
        text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
      }
    }
  }

  @keyframes pulse {
    0%, 100% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.1);
    }
  }

  .learning-content {
    background: white;
    border-radius: 20px;
    padding: 2rem;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2);

    h2 {
      text-align: center;
      font-size: 2.5rem;
      margin-bottom: 2rem;
      color: #333;
    }

    .learning-modules {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
    }

    .module-card {
      background: #f8f9fa;
      border-radius: 15px;
      padding: 1.5rem;
      text-align: center;
      border: 3px solid transparent;
      transition: all 0.3s ease;

      &:hover {
        border-color: @kids-blue;
        transform: translateY(-5px);
        box-shadow: 0 8px 25px rgba(0,0,0,0.15);
      }

      h3 {
        font-size: 1.5rem;
        color: #333;
        margin-bottom: 1rem;
      }

      p {
        color: #666;
        margin-bottom: 1rem;
        line-height: 1.6;
      }

      .example {
        background: #e9ecef;
        padding: 1rem;
        border-radius: 10px;
        font-size: 1.2rem;
        font-weight: bold;
        color: @kids-purple;
        margin-bottom: 1rem;
        border: 2px dashed @kids-blue;
      }

      .practice-btn {
        background: linear-gradient(45deg, @kids-green, @kids-blue);
        color: white;
        border: none;
        padding: 0.8rem 2rem;
        border-radius: 25px;
        font-size: 1rem;
        font-weight: bold;
        cursor: pointer;
        transition: all 0.3s ease;

        &:hover {
          transform: scale(1.05);
          box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
      }
    }
  }

  @media (max-width: 768px) {
    .learning-container {
      padding: 1rem 0;
    }

    .welcome-title {
      font-size: 2rem !important;
    }

    .welcome-subtitle {
      font-size: 1rem !important;
    }

    .subjects-grid {
      grid-template-columns: 1fr;
      gap: 1rem;
    }

    .subject-card {
      padding: 1.5rem;
    }

    .subject-header {
      flex-direction: column;
      gap: 1rem;
      text-align: center;

      .subject-title h1 {
        font-size: 2rem;
      }

      .subject-icon-large {
        font-size: 3rem !important;
      }
    }

    .learning-modules {
      grid-template-columns: 1fr;
    }
  }
</style>