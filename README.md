<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>给你的情人节惊喜</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            background: linear-gradient(135deg, #ff99cc, #ff6699);
            overflow: hidden;
            font-family: 'Microsoft YaHei', sans-serif;
            position: relative;
        }

        .container {
            position: relative;
            z-index: 2;
            text-align: center;
            padding-top: 20%;
        }

        h1 {
            color: #fff;
            font-size: 3rem;
            text-shadow: 0 0 15px rgba(255,51,102,0.5);
            animation: glow 2s ease-in-out infinite;
        }

        .hearts {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .heart {
            position: absolute;
            font-size: 24px;
            color: #ff3366;
            animation: floatDown 6s linear infinite;
            opacity: 0;
        }

        .message-box {
            background: rgba(255,255,255,0.9);
            border-radius: 15px;
            padding: 20px;
            margin: 30px 20px;
            box-shadow: 0 0 20px rgba(255,51,102,0.3);
            transform: scale(0);
            animation: popup 1s 2s forwards;
        }

        /* 按钮容器 */
        .music-button-container {
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            margin: 20px auto;
        }

        /* 引导提示词 */
        .music-button-hint {
            color: #fff;
            font-size: 14px;
            text-shadow: 0 0 10px rgba(255, 51, 102, 0.8);
            animation: hintPulse 2s infinite;
        }

        @keyframes hintPulse {
            0%, 100% { opacity: 0.8; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.1); }
        }

        /* 可爱按钮样式 */
        .music-button {
            width: 80px;
            height: 80px;
            background: #ff3366;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 0 20px rgba(255, 51, 102, 0.5);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .music-button i {
            color: white;
            font-size: 36px;
        }

        /* 按钮跳动动画 */
        @keyframes bounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        /* 粒子特效 */
        .particles {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .particle {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #ff3366;
            border-radius: 50%;
            animation: float 3s linear infinite;
            opacity: 0;
        }

        @keyframes float {
            0% { transform: translateY(0) scale(1); opacity: 1; }
            100% { transform: translateY(-100vh) scale(0); opacity: 0; }
        }

        @keyframes glow {
            0%, 100% { text-shadow: 0 0 15px rgba(255,51,102,0.5); }
            50% { text-shadow: 0 0 30px rgba(255,51,102,0.8); }
        }

        @keyframes floatDown {
            0% { transform: translateY(-100vh); opacity: 1; }
            100% { transform: translateY(100vh); opacity: 0; }
        }

        @keyframes popup {
            0% { transform: scale(0); }
            80% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>情人节快乐 🌸</h1>
        <div class="message-box">
            <p>给最特别的你：</p>
            <p>愿今天的每一刻都充满甜蜜</p>
            <p>像星星一样闪耀 ✨</p>
            <p>—— 永远挺你的好朋友</p>
        </div>
        <!-- 按钮容器 -->
        <div class="music-button-container">
            <div class="music-button-hint">点击播放音乐</div>
            <div class="music-button" id="musicButton">
                <i>▶️</i>
            </div>
        </div>
    </div>
    <div class="hearts" id="hearts"></div>
    <div class="particles" id="particles"></div>

    <!-- 背景音乐 -->
    <audio id="bgm" loop>
        <source src="https://t.doruo.cn/1CqQMewko" type="audio/mpeg">
        您的浏览器不支持音频播放。
    </audio>

    <script>
        // 生成飘动爱心
        function createHearts() {
            const heartsContainer = document.getElementById('hearts');
            for(let i=0; i<50; i++) {
                const heart = document.createElement('div');
                heart.className = 'heart';
                heart.style.left = Math.random() * 100 + '%';
                heart.style.top = Math.random() * -100 + 'vh'; // 从屏幕上方随机位置开始
                heart.style.animationDelay = Math.random() * 6 + 's';
                heart.innerHTML = '❤';
                heartsContainer.appendChild(heart);
            }
        }

        // 播放器逻辑
        const audio = document.getElementById('bgm');
        const musicButton = document.getElementById('musicButton');
        const particlesContainer = document.getElementById('particles');

        // 播放/暂停
        musicButton.addEventListener('click', () => {
            if (audio.paused) {
                audio.play();
                musicButton.innerHTML = '🎵';
                musicButton.style.animation = 'bounce 0.5s infinite'; // 添加跳动动画
                createParticles(); // 添加粒子特效
            } else {
                audio.pause();
                musicButton.innerHTML = '▶️';
                musicButton.style.animation = 'none'; // 移除跳动动画
            }
        });

        // 生成粒子特效
        function createParticles() {
            for (let i = 0; i < 30; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.top = Math.random() * 100 + 'vh';
                particle.style.animationDelay = Math.random() * 2 + 's';
                particlesContainer.appendChild(particle);

                // 粒子消失后移除
                particle.addEventListener('animationend', () => {
                    particle.remove();
                });
            }
        }

        // 初始化
        window.onload = function() {
            createHearts();
        }
    </script>
</body>
</html>
