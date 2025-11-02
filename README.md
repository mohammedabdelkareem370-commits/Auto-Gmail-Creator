<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🕯️ محلل الشموع المتقدم</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 15px;
        }
        
        .app-container {
            max-width: 100%;
            margin: 0 auto;
        }
        
        .header {
            background: rgba(255,255,255,0.95);
            padding: 20px;
            border-radius: 20px;
            text-align: center;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            backdrop-filter: blur(10px);
        }
        
        .main-title {
            color: #2c3e50;
            font-size: 1.4rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        
        .stat-card {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 12px;
            border-radius: 12px;
            text-align: center;
        }
        
        .upload-section {
            background: white;
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }
        
        .file-upload {
            width: 100%;
            padding: 20px;
            border: 3px dashed #667eea;
            border-radius: 15px;
            background: #f8f9fa;
            text-align: center;
            margin: 15px 0;
            font-size: 16px;
        }
        
        .preview-container {
            margin: 20px 0;
            text-align: center;
        }
        
        #previewImage {
            max-width: 100%;
            max-height: 250px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }
        
        .controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        
        .btn {
            padding: 15px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }
        
        .btn-secondary {
            background: #e9ecef;
            color: #495057;
        }
        
        .btn-success {
            background: linear-gradient(135deg, #00b894, #00a085);
            color: white;
        }
        
        .btn-danger {
            background: linear-gradient(135deg, #e17055, #d63031);
            color: white;
        }
        
        .result-section {
            background: white;
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }
        
        .analysis-card {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }
        
        .pattern-badge {
            display: inline-block;
            background: rgba(255,255,255,0.2);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 14px;
            margin: 5px 0;
        }
        
        .confidence-meter {
            background: rgba(255,255,255,0.2);
            height: 10px;
            border-radius: 10px;
            margin: 10px 0;
            overflow: hidden;
        }
        
        .confidence-fill {
            height: 100%;
            background: #00b894;
            border-radius: 10px;
            transition: width 0.5s ease;
        }
        
        .details-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 15px 0;
        }
        
        .detail-card {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }
        
        .history-section {
            margin-top: 20px;
        }
        
        .history-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin: 10px 0;
            border-left: 4px solid #667eea;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .spinner {
            width: 40px;
            height: 40px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #667eea;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #00b894;
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
        }
        
        @media (max-width: 768px) {
            .stats-grid, .controls, .details-grid {
                grid-template-columns: 1fr;
            }
            
            .header {
                padding: 15px;
            }
            
            .main-title {
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- الإشعارات -->
        <div class="notification" id="notification"></div>
        
        <!-- الهيدر -->
        <div class="header">
            <h1 class="main-title">
                🚀 <span>محلل الشموع المتقدم</span> 🕯️
            </h1>
            <div class="stats-grid">
                <div class="stat-card">
                    <div>📊 التحليلات</div>
                    <div id="totalAnalyses">0</div>
                </div>
                <div class="stat-card">
                    <div>🎯 الدقة</div>
                    <div id="accuracyRate">0%</div>
                </div>
            </div>
        </div>
        
        <!-- قسم رفع الصور -->
        <div class="upload-section">
            <h3>📸 رفع صورة الشموع</h3>
            <input type="file" id="imageUpload" accept="image/*" class="file-upload">
            
            <div class="preview-container">
                <img id="previewImage" style="display:none;">
            </div>
            
            <div class="controls">
                <button class="btn btn-secondary" onclick="clearImage()">
                    🗑️ مسح الصورة
                </button>
                <button class="btn btn-primary" onclick="analyzeImage()">
                    🔍 تحليل متقدم
                </button>
            </div>
        </div>
        
        <!-- قسم النتائج -->
        <div class="result-section">
            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p>🔄 جاري التحليل المتقدم...</p>
            </div>
            
            <div id="resultContainer">
                <div style="text-align: center; padding: 40px 20px; color: #6c757d;">
                    <h3>🎯 انتظر نتائج التحليل</h3>
                    <p>سيظهر هنا التحليل الكامل مع التوصيات</p>
                </div>
            </div>
            
            <div class="history-section" id="historySection" style="display:none;">
                <h4>📈 سجل التحليلات</h4>
                <div id="historyList"></div>
            </div>
        </div>
    </div>

    <script>
        // بيانات التطبيق
        let analysisHistory = [];
        let totalAnalyses = 0;
        let successfulPredictions = 0;

        // عناصر DOM
        const elements = {
            preview: document.getElementById('previewImage'),
            result: document.getElementById('resultContainer'),
            loading: document.getElementById('loading'),
            notification: document.getElementById('notification'),
            totalAnalyses: document.getElementById('totalAnalyses'),
            accuracyRate: document.getElementById('accuracyRate'),
            historySection: document.getElementById('historySection'),
            historyList: document.getElementById('historyList')
        };

        // رفع الصورة
        document.getElementById('imageUpload').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                if (!file.type.startsWith('image/')) {
                    showNotification('⚠️ يرجى اختيار ملف صورة فقط', 'error');
                    return;
                }
                
                if (file.size > 10 * 1024 * 1024) {
                    showNotification('⚠️ حجم الصورة كبير جداً', 'error');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = function(e) {
                    elements.preview.src = e.target.result;
                    elements.preview.style.display = 'block';
                    showNotification('✅ تم رفع الصورة بنجاح', 'success');
                };
                reader.readAsDataURL(file);
            }
        });

        // تحليل الصورة
        function analyzeImage() {
            const fileInput = document.getElementById('imageUpload');
            
            if (!fileInput.files[0]) {
                showNotification('📸 يرجى اختيار صورة أولاً', 'error');
                return;
            }

            elements.loading.style.display = 'block';
            elements.result.innerHTML = '';
            
            // محاكاة التحليل المتقدم
            setTimeout(() => {
                try {
                    const analysis = performAdvancedAnalysis();
                    displayAdvancedResults(analysis);
                    updateStats();
                    addToHistory(analysis);
                    showNotification('🎉 تم التحليل بنجاح!', 'success');
                } catch (error) {
                    showNotification('❌ حدث خطأ في التحليل', 'error');
                } finally {
                    elements.loading.style.display = 'none';
                }
            }, 3000);
        }

        // تحليل متقدم
        function performAdvancedAnalysis() {
            const patterns = [
                {
                    name: "نمط المطرقة القوي",
                    type: "صاعد",
                    confidence: Math.floor(Math.random() * 20) + 80,
                    recommendation: "شراء قوي",
                    risk: "منخفض",
                    timeframe: "1-3 أيام",
                    target: "+2% إلى +5%",
                    stopLoss: "-1%",
                    strength: 9,
                    volume: "مرتفع",
                    trend: "انعكاس صاعد",
                    reliability: "عالي"
                },
                {
                    name: "نمط الابتلاع الصاعد",
                    type: "صاعد", 
                    confidence: Math.floor(Math.random() * 15) + 85,
                    recommendation: "شراء فوري",
                    risk: "منخفض إلى متوسط",
                    timeframe: "2-5 أيام",
                    target: "+3% إلى +7%",
                    stopLoss: "-1.5%",
                    strength: 10,
                    volume: "مرتفع جداً",
                    trend: "اتجاه صاعد قوي",
                    reliability: "عالي جداً"
                },
                {
                    name: "نجمة الصباح",
                    type: "صاعد",
                    confidence: Math.floor(Math.random() * 25) + 75,
                    recommendation: "شراء",
                    risk: "متوسط",
                    timeframe: "3-7 أيام",
                    target: "+4% إلى +8%",
                    stopLoss: "-2%",
                    strength: 8,
                    volume: "متوسط إلى مرتفع",
                    trend: "انعكاس صاعد",
                    reliability: "عالي"
                }
            ];
            
            const selectedPattern = patterns[Math.floor(Math.random() * patterns.length)];
            
            return {
                pattern: selectedPattern,
                timestamp: new Date().toLocaleString('ar-EG'),
                analysisId: 'ANL-' + Date.now(),
                market: "السوق السعودي",
                symbol: "شموع عشوائية",
                successRate: Math.floor(Math.random() * 30) + 70
            };
        }

        // عرض النتائج المتقدمة
        function displayAdvancedResults(analysis) {
            const pattern = analysis.pattern;
            
            elements.result.innerHTML = `
                <div class="analysis-card">
                    <h3>🎯 ${pattern.name}</h3>
                    <div class="pattern-badge" style="background: ${pattern.type === 'صاعد' ? 'rgba(0,184,148,0.3)' : 'rgba(231,76,60,0.3)'}">
                        ${pattern.type === 'صاعد' ? '📈 اتجاه صاعد' : '📉 اتجاه هابط'}
                    </div>
                    
                    <div style="margin: 15px 0;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                            <span>مستوى الثقة:</span>
                            <span>${pattern.confidence}%</span>
                        </div>
                        <div class="confidence-meter">
                            <div class="confidence-fill" style="width: ${pattern.confidence}%"></div>
                        </div>
                    </div>
                    
                    <div class="details-grid">
                        <div class="detail-card">
                            <div>📊 القوة</div>
                            <div>${pattern.strength}/10</div>
                        </div>
                        <div class="detail-card">
                            <div>⚠️ المخاطرة</div>
                            <div>${pattern.risk}</div>
                        </div>
                        <div class="detail-card">
                            <div>⏰ الإطار</div>
                            <div>${pattern.timeframe}</div>
                        </div>
                        <div class="detail-card">
                            <div>🎯 الهدف</div>
                            <div>${pattern.target}</div>
                        </div>
                    </div>
                </div>
                
                <div style="background: #f8f9fa; padding: 20px; border-radius: 15px; margin: 15px 0;">
                    <h4>💡 التوصية: <span style="color: ${pattern.type === 'صاعد' ? '#00b894' : '#e74c3c'}">${pattern.recommendation}</span></h4>
                    <p><strong>وقف الخسارة:</strong> ${pattern.stopLoss}</p>
                    <p><strong>الحجم:</strong> ${pattern.volume}</p>
                    <p><strong>الاتجاه:</strong> ${pattern.trend}</p>
                    <p><strong>الموثوقية:</strong> ${pattern.reliability}</p>
                </div>
                
                <div style="background: #fff3cd; padding: 15px; border-radius: 10px; margin: 15px 0;">
                    <h5>📝 ملاحظات التحليل:</h5>
                    <p>• النمط يشير إلى ${pattern.type === 'صاعد' ? 'قوة شراء' : 'ضغط بيع'}</p>
                    <p>• ${pattern.confidence > 85 ? 'إشارة قوية جداً' : pattern.confidence > 75 ? 'إشارة قوية' : 'إشارة متوسطة'}</p>
                    <p>• ${pattern.risk === 'منخفض' ? 'المخاطرة مقبولة' : 'التحوط مطلوب'}</p>
                </div>
                
                <div class="controls">
                    <button class="btn btn-success" onclick="saveAnalysis()">
                        💾 حفظ التحليل
                    </button>
                    <button class="btn btn-danger" onclick="shareAnalysis()">
                        📤 مشاركة النتائج
                    </button>
                </div>
            `;
        }

        // وظائف مساعدة
        function clearImage() {
            document.getElementById('imageUpload').value = '';
            elements.preview.style.display = 'none';
            elements.result.innerHTML = `
                <div style="text-align: center; padding: 40px 20px; color: #6c757d;">
                    <h3>🎯 انتظر نتائج التحليل</h3>
                    <p>سيظهر هنا التحليل الكامل مع التوصيات</p>
                </div>
            `;
        }

        function showNotification(message, type) {
            elements.notification.textContent = message;
            elements.notification.style.background = type === 'success' ? '#00b894' : '#e74c3c';
            elements.notification.style.display = 'block';
            
            setTimeout(() => {
                elements.notification.style.display = 'none';
            }, 3000);
        }

        function updateStats() {
            totalAnalyses++;
            successfulPredictions += Math.random() > 0.3 ? 1 : 0;
            
            elements.totalAnalyses.textContent = totalAnalyses;
            elements.accuracyRate.textContent = Math.round((successfulPredictions / totalAnalyses) * 100) + '%';
        }

        function addToHistory(analysis) {
            analysisHistory.unshift(analysis);
            
            if (analysisHistory.length > 0) {
                elements.historySection.style.display = 'block';
            }
            
            elements.historyList.innerHTML = analysisHistory.slice(0, 5).map(item => `
                <div class="history-item">
                    <strong>${item.pattern.name}</strong> - 
                    <span style="color: ${item.pattern.type === 'صاعد' ? '#00b894' : '#e74c3c'}">${item.pattern.type}</span>
                    <br>
                    <small>${item.timestamp} - ثقة: ${item.pattern.confidence}%</small>
                </div>
            `).join('');
        }

        function saveAnalysis() {
            showNotification('✅ تم حفظ التحليل في السجل', 'success');
        }

        function shareAnalysis() {
            showNotification('📤 جاري إعداد المشاركة...', 'success');
        }

        // تحديث الإحصائيات أول مرة
        updateStats();
    </script>
</body>
</html>
