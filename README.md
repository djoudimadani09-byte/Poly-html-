<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Polylang Hub - منصة الترجمة الذكية</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap');
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Tajawal', sans-serif; }
    body { background-color: #f8f9fa; direction: rtl; color: #333; display: flex; justify-content: center; align-items: center; min-height: 100vh; padding: 20px; }
    .app-container { width: 100%; max-width: 400px; display: flex; flex-direction: column; align-items: center; transition: all 0.3s ease; }
    .brand-header { text-align: center; margin-bottom: 24px; width: 100%; }
    .logo-box { width: 75px; height: 75px; background: linear-gradient(135deg, #e53935, #b71c1c); color: white; display: flex; justify-content: center; align-items: center; border-radius: 20px; margin: 0 auto 12px auto; box-shadow: 0 10px 20px rgba(229, 57, 53, 0.3); font-size: 36px; font-weight: 800; }
    .brand-header h1 { font-size: 24px; color: #1a1a1a; font-weight: 700; }
    .brand-header p { font-size: 14px; color: #666; margin-top: 4px; }
    .login-card { background: white; padding: 28px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05); border: 1px solid #eaeaea; width: 100%; }
    .login-card h2 { font-size: 18px; margin-bottom: 20px; color: #222; }
    .tabs { display: flex; background: #f1f3f5; border-radius: 10px; padding: 4px; margin-bottom: 20px; }
    .tab-btn { flex: 1; background: transparent; border: none; padding: 8px; font-weight: 600; color: #666; cursor: pointer; border-radius: 8px; font-family: 'Tajawal'; }
    .tab-btn.active { background: white; color: #e53935; box-shadow: 0 2px 8px rgba(0,0,0,0.05); }
    .input-group { margin-bottom: 16px; text-align: right; }
    .input-group label { display: block; font-size: 13px; color: #555; margin-bottom: 6px; font-weight: 500; }
    .input-group input, .input-group select, .input-group textarea { width: 100%; padding: 12px 14px; border: 1.5px solid #ddd; border-radius: 10px; font-size: 14px; outline: none; transition: all 0.3s; font-family: 'Tajawal'; }
    .input-group input:focus, .input-group select:focus, .input-group textarea:focus { border-color: #e53935; box-shadow: 0 0 0 3px rgba(229, 57, 53, 0.1); }
    .btn-primary { width: 100%; padding: 13px; background-color: #e53935; color: white; border: none; border-radius: 10px; font-size: 15px; font-weight: 700; cursor: pointer; transition: background 0.3s; margin-top: 10px; font-family: 'Tajawal'; }
    .btn-primary:hover { background-color: #b71c1c; }
    .output-box { margin-top: 18px; padding: 12px; background: #f1f3f5; border-radius: 8px; font-size: 12px; color: #444; word-break: break-all; text-align: center; border: 1px dashed #ced4da; }
  </style>
</head>
<body>

  <div class="app-container">
    <div class="brand-header">
      <div class="logo-box">P</div>
      <h1>Polylang Hub</h1>
      <p>منصة الترجمة الذكية والمعتمدة</p>
    </div>

    <div class="login-card">
      <div class="tabs">
        <button id="tabLogin" class="tab-btn active" onclick="switchTab('login')">دخول</button>
        <button id="tabRegister" class="tab-btn" onclick="switchTab('register')">حساب جديد</button>
      </div>

      <div id="loginForm">
        <h2>تسجيل الدخول</h2>
        <div class="input-group">
          <label>البريد الإلكتروني</label>
          <input type="email" id="loginEmail" placeholder="name@example.com" />
        </div>
        <div class="input-group">
          <label>كلمة المرور</label>
          <input type="password" id="loginPassword" placeholder="••••••••" />
        </div>
        <button class="btn-primary" onclick="sendLogin()">تسجيل الدخول</button>
      </div>

      <div id="registerForm" style="display: none;">
        <h2>إنشاء حساب جديد</h2>
        <div class="input-group">
          <label>الاسم الكامل</label>
          <input type="text" id="regName" placeholder="اسمك الكريم" />
        </div>
        <div class="input-group">
          <label>البريد الإلكتروني</label>
          <input type="email" id="regEmail" placeholder="name@example.com" />
        </div>
        <div class="input-group">
          <label>كلمة المرور</label>
          <input type="password" id="regPassword" placeholder="••••••••" />
        </div>
        <div class="input-group">
          <label>نوع الحساب</label>
          <select id="regRole">
            <option value="CLIENT">زبون (Client)</option>
            <option value="TRANSLATOR">مترجم (Translator)</option>
          </select>
        </div>
        <button class="btn-primary" onclick="sendRegister()">إنشاء الحساب</button>
      </div>
      
      <div id="result" class="output-box">جاهز للاتصال بالسيرفر السحابي...</div>
    </div>
  </div>

  <script>
    function switchTab(tab) {
      const loginForm = document.getElementById('loginForm');
      const registerForm = document.getElementById('registerForm');
      const tabLogin = document.getElementById('tabLogin');
      const tabRegister = document.getElementById('tabRegister');
      
      if(tab === 'login') {
        loginForm.style.display = 'block';
        registerForm.style.display = 'none';
        tabLogin.classList.add('active');
        tabRegister.classList.remove('active');
      } else {
        loginForm.style.display = 'none';
        registerForm.style.display = 'block';
        tabRegister.classList.add('active');
        tabLogin.classList.remove('active');
      }
    }

    async function sendLogin() {
      const email = document.getElementById('loginEmail').value;
      const password = document.getElementById('loginPassword').value;
      const resultDiv = document.getElementById('result');
      
      if(!email || !password) {
        resultDiv.style.color = "#e53935";
        resultDiv.innerText = "الرجاء إدخال البريد وكلمة المرور";
        return;
      }

      resultDiv.style.color = "#333";
      resultDiv.innerText = "جاري إرسال طلب الدخول للسيرفر...";

      try {
        const response = await fetch('https://polylang-hub.onrender.com/api/v1/auth/login', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ email, password })
        });

        const data = await response.json();
        
        if (response.ok) {
          showProDashboard(data.user, data.access_token);
        } else {
          resultDiv.style.color = "#e65100";
          resultDiv.innerText = "⚠ رد السيرفر: " + (data.message || JSON.stringify(data));
        }
      } catch (error) {
        resultDiv.style.color = "#e53935";
        resultDiv.innerText = "❌ خطأ في الاتصال: " + error;
      }
    }

    async function sendRegister() {
      const name = document.getElementById('regName').value;
      const email = document.getElementById('regEmail').value;
      const password = document.getElementById('regPassword').value;
      const role = document.getElementById('regRole').value;
      const resultDiv = document.getElementById('result');
      
      if(!name || !email || !password) {
        resultDiv.style.color = "#e53935";
        resultDiv.innerText = "الرجاء ملء جميع الحقول لإنشاء الحساب";
        return;
      }

      resultDiv.style.color = "#333";
      resultDiv.innerText = "جاري إنشاء الحساب في قاعدة البيانات...";

      try {
        const response = await fetch('https://polylang-hub.onrender.com/api/v1/auth/register', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ name, email, password, role })
        });

        const data = await response.json();
        
        if (response.ok) {
          resultDiv.style.color = "#2e7d32";
          resultDiv.innerText = "✓ تم إنشاء الحساب بنجاح! انتقل لتبويب دخول وسجل الآن.";
        } else {
          resultDiv.style.color = "#e65100";
          resultDiv.innerText = "⚠ رد السيرفر: " + (data.message || JSON.stringify(data));
        }
      } catch (error) {
        resultDiv.style.color = "#e53935";
        resultDiv.innerText = "❌ خطأ في الاتصال: " + error;
      }
    }

    function showProDashboard(user, token) {
      const container = document.querySelector('.app-container');
      container.style.maxWidth = '650px';
      
      container.innerHTML = `
        <div class="login-card" style="width: 100%; text-align: right;">
          <div style="display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #f1f3f5; padding-bottom: 15px; margin-bottom: 20px;">
            <div>
              <h2 style="color: #1a1a1a; font-size: 20px; margin-bottom: 2px;">⚡ مرحباً، ${user.name}</h2>
              <span style="font-size: 11px; background: #ffebee; color: #c62828; padding: 3px 10px; border-radius: 6px; font-weight: 700;">حساب ${user.role} معتمد</span>
            </div>
            <button onclick="resetApp()" style="background: #f1f3f5; border: none; padding: 8px 12px; border-radius: 8px; font-family: 'Tajawal'; font-size: 13px; cursor: pointer; color: #d32f2f; font-weight: 600;">تسجيل خروج</button>
          </div>

          <div style="margin-bottom: 20px;">
            <label style="display: block; font-size: 14px; font-weight: 700; color: #333; margin-bottom: 10px;">اختر قطاع الخدمة المتخصصة:</label>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
              <button onclick="setServiceType('text')" id="srvText" class="srv-btn" style="padding: 10px; border-radius: 8px; border: 1.5px solid #e53935; background: #ffebee; color: #e53935; font-weight: 700; cursor: pointer; font-family: 'Tajawal'; font-size: 13px;">📝 ترجمة مستندات ونصية</button>
              <button onclick="setServiceType('video')" id="srvVideo" class="srv-btn" style="padding: 10px; border-radius: 8px; border: 1.5px solid #ddd; background: white; color: #666; font-weight: 600; cursor: pointer; font-family: 'Tajawal'; font-size: 13px;">🎬 ترجمة ودبلجة فيديوهات</button>
            </div>
          </div>

          <div style="background: #fafafa; padding: 16px; border-radius: 12px; border: 1px solid #eaeaea; margin-bottom: 20px;">
            <div id="formDynamicContent">
              <h3 style="font-size: 15px; color: #333; margin-bottom: 12px;">إرسال ملف أو نص للترجمة الدقيقة</h3>
              <div class="input-group">
                <label>اتجاة ونطاق اللغات</label>
                <input type="text" id="orderPair" placeholder="مثال: من الفرنسية إلى العربية (FR -> AR)" />
              </div>
              <div class="input-group">
                <label>المحتوى أو الرابط</label>
                <textarea id="orderDesc" rows="3" placeholder="أدخل النص أو رابط الفيديو..." style="width: 100%; padding: 12px; border: 1.5px solid #ddd; border-radius: 10px; font-family: 'Tajawal'; outline: none; resize: none;"></textarea>
              </div>
            </div>
            
            <div class="input-group" style="margin-top: 10px;">
              <label>مستوى الأفضلية والسرعة</label>
              <select id="orderSpeed" style="width: 100%; padding: 10px; border: 1.5px solid #ddd; border-radius: 8px; font-family: 'Tajawal'; background: white;">
                <option value="standard">قياسي (دقة عالية - خلال 24 ساعة)</option>
                <option value="express">سريع جداً / Express (أولوية قصوى +25%)</option>
              </select>
            </div>

            <button class="btn-primary" onclick="submitProOrder()" style="margin-top: 15px;">إرسال الطلب وإصدار الفاتورة الذكية</button>
          </div>

          <div>
            <h3 style="font-size: 15px; color: #333; margin-bottom: 10px;">سجل مشاريعك وطلباتك النشطة</h3>
            <div id="proOrdersList" style="background: #f1f3f5; padding: 16px; border-radius: 10px; text-align: center; color: #666; font-size: 13px; border: 1px dashed #ced4da;">
              لا توجد طلبات نشطة حالياً. ابدأ بإرسال مشروعك الأول!
            </div>
          </div>
        </div>
      `;
    }

    let currentService = 'text';
    function setServiceType(type) {
      currentService = type;
      const srvText = document.getElementById('srvText');
      const srvVideo = document.getElementById('srvVideo');
      const content = document.getElementById('formDynamicContent');

      if(type === 'text') {
        srvText.style.background = "#ffebee"; srvText.style.color = "#e53935"; srvText.style.borderColor = "#e53935";
        srvVideo.style.background = "white"; srvVideo.style.color = "#666"; srvVideo.style.borderColor = "#ddd";
        content.innerHTML = `
          <h3 style="font-size: 15px; color: #333; margin-bottom: 12px;">إرسال ملف أو نص للترجمة القانونية والتقنية</h3>
          <div class="input-group">
            <label>اتجاه اللغات</label>
            <input type="text" id="orderPair" placeholder="مثال: من العربية للألمانية (AR -> DE)" />
          </div>
          <div class="input-group">
            <label>النص أو تفاصيل الملف</label>
            <textarea id="orderDesc" rows="3" placeholder="اكتب النص المراد ترجمته هنا..." style="width: 100%; padding: 12px; border: 1.5px solid #ddd; border-radius: 10px; font-family: 'Tajawal'; outline: none; resize: none;"></textarea>
          </div>
        `;
      } else {
        srvVideo.style.background = "#ffebee"; srvVideo.style.color = "#e53935"; srvVideo.style.borderColor = "#e53935";
        srvText.style.background = "white"; srvText.style.color = "#666"; srvText.style.borderColor = "#ddd";
        content.innerHTML = `
          <h3 style="font-size: 15px; color: #333; margin-bottom: 12px;">ترجمة ودبلجة ملفات الفيديو وملفات التوقيت (SRT)</h3>
          <div class="input-group">
            <label>رابط الفيديو أو اللغات المستهدفة</label>
            <input type="text" id="orderPair" placeholder="رابط الفيديو (يوتيوب وغيرها)" />
          </div>
          <div class="input-group">
            <label>مواصفات الترجمة المرئية</label>
            <textarea id="orderDesc" rows="3" placeholder="نوع الترجمة المرئية أو تفاصيل الدبلجة..." style="width: 100%; padding: 12px; border: 1.5px solid #ddd; border-radius: 10px; font-family: 'Tajawal'; outline: none; resize: none;"></textarea>
          </div>
        `;
      }
    }

    function submitProOrder() {
      const pair = document.getElementById('orderPair').value;
      const desc = document.getElementById('orderDesc').value;
      const speed = document.getElementById('orderSpeed').value;
      const list = document.getElementById('proOrdersList');

      if(!pair || !desc) {
        alert("الرجاء ملء حقول اللغات والتفاصيل المطلوبة");
        return;
      }

      const serviceLabel = currentService === 'text' ? '📝 ترجمة مستند' : '🎬 ترجمة فيديو';
      const speedLabel = speed === 'express' ? '⚡ سريع جداً (Express)' : '🛡 قياسي معتمد';

      list.innerHTML = `
        <div style="background: white; padding: 12px; border-radius: 10px; text-align: right; border: 1px solid #ddd;">
          <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 6px;">
            <span style="font-weight: 700; color: #e53935; font-size: 14px;">${serviceLabel}: ${pair}</span>
            <span style="font-size: 10px; background: #e8f5e9; color: #2e7d32; padding: 2px 6px; border-radius: 4px; font-weight: bold;">قيد المعالجة</span>
          </div>
          <p style="color: #444; font-size: 12px; margin-bottom: 6px;">التفاصيل: ${desc}</p>
          <div style="font-size: 11px; color: #666; border-top: 1px solid #f1f3f5; padding-top: 6px; display: flex; justify-content: space-between;">
            <span>الأولوية: <strong>${speedLabel}</strong></span>
            <span style="color: #1976d2; font-weight: bold;">جاري ربط المترجم...</span>
          </div>
        </div>
      `;
      alert("تم إرسال المشروع بنجاح إلى شبكة المترجمين!");
    }

    function resetApp() {
      window.open(window.location.href, "_self");
    }
  </script>
</body>
</html>
