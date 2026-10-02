<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>⚡ ماشین حساب نئونی خفن ⚡</title>
  <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet" type="text/css" />
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #000000;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Vazirmatn', sans-serif;
      overflow: hidden;
    }

    /* ذرات پس‌زمینه */
    .particles {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 0;
    }

    .particle {
      position: absolute;
      border-radius: 50%;
      animation: float linear infinite;
      opacity: 0;
    }

    @keyframes float {
      0% {
        transform: translateY(100vh) scale(0);
        opacity: 0;
      }
      10% {
        opacity: 1;
      }
      90% {
        opacity: 1;
      }
      100% {
        transform: translateY(-100vh) scale(1);
        opacity: 0;
      }
    }

    /* کانتینر اصلی */
    .calculator-container {
      position: relative;
      z-index: 1;
      perspective: 1000px;
    }

    /* هاله بیرونی */
    .glow-ring {
      position: absolute;
      inset: -8px;
      border-radius: 30px;
      background: conic-gradient(from 0deg, 
        #ff00ff, #00ffff, #ff00ff, #ff0000, 
        #ffff00, #00ff00, #00ffff, #ff00ff);
      filter: blur(20px);
      opacity: 0.8;
      animation: rotateGlow 4s linear infinite;
      z-index: -1;
    }

    @keyframes rotateGlow {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    /* بدنه ماشین حساب */
    .calculator {
      background: rgba(10, 10, 15, 0.95);
      backdrop-filter: blur(20px);
      border-radius: 24px;
      padding: 25px;
      width: 380px;
      border: 2px solid rgba(255, 0, 255, 0.3);
      box-shadow: 
        0 0 40px rgba(255, 0, 255, 0.3),
        0 0 80px rgba(0, 255, 255, 0.2),
        0 0 120px rgba(255, 0, 255, 0.1),
        inset 0 0 40px rgba(255, 0, 255, 0.05);
      position: relative;
      animation: borderPulse 3s ease-in-out infinite;
    }

    @keyframes borderPulse {
      0%, 100% { border-color: rgba(255, 0, 255, 0.3); }
      50% { border-color: rgba(0, 255, 255, 0.5); }
    }

    /* عنوان */
    .title {
      text-align: center;
      color: #fff;
      font-size: 14px;
      margin-bottom: 15px;
      text-transform: uppercase;
      letter-spacing: 4px;
      text-shadow: 
        0 0 10px #ff00ff,
        0 0 20px #ff00ff,
        0 0 40px #ff00ff;
      animation: titleFlicker 2s ease-in-out infinite;
    }

    @keyframes titleFlicker {
      0%, 19%, 21%, 23%, 25%, 54%, 56%, 100% {
        opacity: 1;
      }
      20%, 24%, 55% {
        opacity: 0.4;
      }
    }

    /* نمایشگر */
    .display {
      background: rgba(0, 0, 0, 0.8);
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 20px;
      text-align: left;
      direction: ltr;
      border: 1px solid rgba(0, 255, 255, 0.4);
      box-shadow: 
        inset 0 0 20px rgba(0, 255, 255, 0.1),
        0 0 30px rgba(0, 255, 255, 0.2);
      position: relative;
      overflow: hidden;
    }

    .display::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, 
        transparent, 
        rgba(0, 255, 255, 0.1), 
        transparent);
      animation: scanLine 3s linear infinite;
    }

    @keyframes scanLine {
      0% { left: -100%; }
      100% { left: 100%; }
    }

    .display-text {
      color: #00ffff;
      font-size: 36px;
      font-weight: bold;
      text-shadow: 
        0 0 10px #00ffff,
        0 0 20px #00ffff,
        0 0 40px #00ffff,
        0 0 80px #00ffff;
      min-height: 50px;
      word-wrap: break-word;
      position: relative;
      z-index: 1;
      font-family: 'Courier New', 'Vazirmatn', monospace;
    }

    /* دکمه‌ها */
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }

    .btn {
      background: rgba(20, 20, 30, 0.9);
      border: 1px solid rgba(255, 0, 255, 0.3);
      color: #fff;
      font-size: 22px;
      padding: 18px;
      border-radius: 14px;
      cursor: pointer;
      transition: all 0.2s ease;
      position: relative;
      overflow: hidden;
      font-family: 'Vazirmatn', sans-serif;
      font-weight: bold;
      text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
    }

    .btn::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: radial-gradient(circle, rgba(255, 0, 255, 0.3) 0%, transparent 70%);
      opacity: 0;
      transition: opacity 0.3s;
    }

    .btn:hover {
      transform: translateY(-3px);
      border-color: #ff00ff;
      box-shadow: 
        0 5px 20px rgba(255, 0, 255, 0.5),
        0 0 40px rgba(255, 0, 255, 0.3);
      color: #ff00ff;
      text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
    }

    .btn:hover::before {
      opacity: 1;
    }

    .btn:active {
      transform: translateY(0) scale(0.95);
      box-shadow: 
        0 2px 10px rgba(255, 0, 255, 0.8),
        0 0 30px rgba(255, 0, 255, 0.6);
      transition: all 0.05s;
    }

    /* دکمه‌های خاص */
    .btn-operator {
      background: rgba(255, 0, 255, 0.2);
      border-color: rgba(255, 0, 255, 0.6);
      color: #ff00ff;
      text-shadow: 0 0 10px #ff00ff;
    }

    .btn-operator:hover {
      background: rgba(255, 0, 255, 0.4);
      box-shadow: 
        0 0 30px rgba(255, 0, 255, 0.8),
        0 0 60px rgba(255, 0, 255, 0.4);
    }

    .btn-equals {
      background: linear-gradient(135deg, rgba(255, 0, 255, 0.6), rgba(0, 255, 255, 0.6));
      border-color: rgba(0, 255, 255, 0.8);
      font-size: 28px;
      color: #fff;
      text-shadow: 0 0 15px #fff;
      grid-row: span 1;
      animation: equalsGlow 2s ease-in-out infinite;
    }

    @keyframes equalsGlow {
      0%, 100% { 
        box-shadow: 0 0 20px rgba(0, 255, 255, 0.5);
      }
      50% { 
        box-shadow: 0 0 40px rgba(255, 0, 255, 0.8), 0 0 80px rgba(0, 255, 255, 0.6);
      }
    }

    .btn-equals:hover {
      transform: translateY(-3px) scale(1.05);
      box-shadow: 
        0 0 50px rgba(255, 0, 255, 0.9),
        0 0 100px rgba(0, 255, 255, 0.7),
        0 0 150px rgba(255, 0, 255, 0.5);
    }

    .btn-clear {
      background: rgba(255, 50, 50, 0.2);
      border-color: rgba(255, 50, 50, 0.6);
      color: #ff3333;
      text-shadow: 0 0 10px #ff0000;
    }

    .btn-clear:hover {
      background: rgba(255, 50, 50, 0.4);
      box-shadow: 0 0 30px rgba(255, 0, 0, 0.8);
    }

    .btn-zero {
      grid-column: span 2;
    }

    /* انیمیشن کلیک */
    .ripple {
      position: absolute;
      border-radius: 50%;
      background: rgba(255, 0, 255, 0.6);
      transform: scale(0);
      animation: rippleEffect 0.6s ease-out;
      pointer-events: none;
    }

    @keyframes rippleEffect {
      to {
        transform: scale(4);
        opacity: 0;
      }
    }

    /* واکنش‌گرایی */
    @media (max-width: 420px) {
      .calculator {
        width: 95vw;
        padding: 18px;
      }
      .btn {
        font-size: 18px;
        padding: 14px;
      }
      .display-text {
        font-size: 28px;
      }
    }
  </style>
</head>
<body>

  <!-- ذرات پس‌زمینه -->
  <div class="particles" id="particles"></div>

  <!-- کانتینر ماشین حساب -->
  <div class="calculator-container">
    <div class="glow-ring"></div>
    <div class="calculator">
      <div class="title">⚡ NEON CALC ⚡</div>
      <div class="display">
        <div class="display-text" id="display">0</div>
      </div>
      <div class="buttons">
        <button class="btn btn-clear" onclick="clearAll()">C</button>
        <button class="btn btn-operator" onclick="appendValue('(')">(</button>
        <button class="btn btn-operator" onclick="appendValue(')')">)</button>
        <button class="btn btn-operator" onclick="appendValue('/')">÷</button>
        
        <button class="btn" onclick="appendValue('7')">7</button>
        <button class="btn" onclick="appendValue('8')">8</button>
        <button class="btn" onclick="appendValue('9')">9</button>
        <button class="btn btn-operator" onclick="appendValue('*')">×</button>
        
        <button class="btn" onclick="appendValue('4')">4</button>
        <button class="btn" onclick="appendValue('5')">5</button>
        <button class="btn" onclick="appendValue('6')">6</button>
        <button class="btn btn-operator" onclick="appendValue('-')">−</button>
        
        <button class="btn" onclick="appendValue('1')">1</button>
        <button class="btn" onclick="appendValue('2')">2</button>
        <button class="btn" onclick="appendValue('3')">3</button>
        <button class="btn btn-operator" onclick="appendValue('+')">+</button>
        
        <button class="btn btn-zero" onclick="appendValue('0')">0</button>
        <button class="btn" onclick="appendValue('.')">.</button>
        <button class="btn btn-equals" onclick="calculate()">=</button>
      </div>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');
    let currentInput = '0';
    let shouldResetDisplay = false;

    // ذرات پس‌زمینه
    function createParticles() {
      const container = document.getElementById('particles');
      const colors = ['#ff00ff', '#00ffff', '#ff0000', '#ffff00', '#00ff00', '#ff8800'];
      
      for (let i = 0; i < 50; i++) {
        const particle = document.createElement('div');
        particle.className = 'particle';
        const size = Math.random() * 4 + 2;
        const color = colors[Math.floor(Math.random() * colors.length)];
        
        particle.style.cssText = `
          width: ${size}px;
          height: ${size}px;
          background: ${color};
          box-shadow: 0 0 ${size * 4}px ${color}, 0 0 ${size * 8}px ${color};
          left: ${Math.random() * 100}%;
          animation-duration: ${Math.random() * 8 + 5}s;
          animation-delay: ${Math.random() * 5}s;
        `;
        
        container.appendChild(particle);
      }
    }

    // افکت ریپل روی دکمه‌ها
    document.querySelectorAll('.btn').forEach(button => {
      button.addEventListener('click', function(e) {
        const ripple = document.createElement('span');
        ripple.className = 'ripple';
        
        const rect = this.getBoundingClientRect();
        const size = Math.max(rect.width, rect.height);
        ripple.style.width = ripple.style.height = size + 'px';
        ripple.style.left = (e.clientX - rect.left - size / 2) + 'px';
        ripple.style.top = (e.clientY - rect.top - size / 2) + 'px';
        
        this.appendChild(ripple);
        
        ripple.addEventListener('animationend', () => {
          ripple.remove();
        });
      });
    });

    function appendValue(value) {
      if (shouldResetDisplay && '0123456789.'.includes(value)) {
        currentInput = '';
        shouldResetDisplay = false;
      }
      
      if (currentInput === '0' && value !== '.') {
        currentInput = value;
      } else {
        currentInput += value;
      }
      
      updateDisplay();
    }

    function updateDisplay() {
      let displayValue = currentInput;
      // جایگزینی عملگرها برای نمایش
      displayValue = displayValue.replace(/\*/g, '×').replace(/\//g, '÷');
      display.textContent = displayValue || '0';
      
      // افکت درخشش نمایشگر
      display.style.textShadow = `
        0 0 10px #00ffff,
        0 0 20px #00ffff,
        0 0 40px #00ffff,
        0 0 80px #00ffff
      `;
      
      setTimeout(() => {
        display.style.textShadow = `
          0 0 10px #00ffff,
          0 0 20px #00ffff,
          0 0 40px #00ffff
        `;
      }, 100);
    }

    function clearAll() {
      currentInput = '0';
      shouldResetDisplay = false;
      updateDisplay();
      
      // افکت فلش روی نمایشگر
      display.style.color = '#ff00ff';
      setTimeout(() => {
        display.style.color = '#00ffff';
      }, 200);
    }

    function calculate() {
      try {
        let expression = currentInput;
        // تبدیل نمادها به عملگرهای واقعی
        expression = expression.replace(/×/g, '*').replace(/÷/g, '/');
        
        // بررسی امنیتی
        if (!/^[0-9+\-*/().\s]*$/.test(expression)) {
          throw new Error('Invalid input');
        }
        
        const result = eval(expression);
        
        if (result === Infinity || result === -Infinity) {
          currentInput = 'خطا';
          display.style.color = '#ff0000';
          setTimeout(() => {
            display.style.color = '#00ffff';
            currentInput = '0';
            updateDisplay();
          }, 1500);
        } else if (isNaN(result)) {
          currentInput = 'خطا';
          display.style.color = '#ff0000';
          setTimeout(() => {
            display.style.color = '#00ffff';
            currentInput = '0';
            updateDisplay();
          }, 1500);
        } else {
          currentInput = Number(result.toFixed(10)).toString();
          shouldResetDisplay = true;
          
          // افکت فلش سبز برای نتیجه موفق
          display.style.color = '#00ff00';
          display.style.textShadow = `
            0 0 20px #00ff00,
            0 0 40px #00ff00,
            0 0 80px #00ff00,
            0 0 120px #00ff00
          `;
          
          setTimeout(() => {
            display.style.color = '#00ffff';
            display.style.textShadow = `
              0 0 10px #00ffff,
              0 0 20px #00ffff,
              0 0 40px #00ffff
            `;
          }, 500);
        }
        
        updateDisplay();
      } catch (error) {
        currentInput = 'خطا';
        display.style.color = '#ff0000';
        updateDisplay();
        
        setTimeout(() => {
          display.style.color = '#00ffff';
          currentInput = '0';
          updateDisplay();
        }, 1500);
      }
    }

    // پشتیبانی از کیبورد
    document.addEventListener('keydown', (e) => {
      const key = e.key;
      
      if ('0123456789.'.includes(key)) {
        appendValue(key);
      } else if (key === '+') appendValue('+');
      else if (key === '-') appendValue('-');
      else if (key === '*') appendValue('*');
      else if (key === '/') {
        e.preventDefault();
        appendValue('/');
      }
      else if (key === '(') appendValue('(');
      else if (key === ')') appendValue(')');
      else if (key === 'Enter' || key === '=') {
        e.preventDefault();
        calculate();
      }
      else if (key === 'Escape' || key === 'c' || key === 'C') {
        clearAll();
      }
      else if (key === 'Backspace') {
        if (currentInput.length > 1) {
          currentInput = currentInput.slice(0, -1);
        } else {
          currentInput = '0';
        }
        updateDisplay();
      }
    });

    // راه‌اندازی ذرات
    createParticles();

    // افکت راه‌اندازی
    window.addEventListener('load', () => {
      display.style.color = '#ff00ff';
      setTimeout(() => {
        display.style.color = '#00ffff';
      }, 600);
    });
  </script>
</body>
</html>
