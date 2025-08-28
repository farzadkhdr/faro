<!DOCTYPE html>
<html lang="ku">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>سیستەمی یەکگرتوو - هۆست لەسەر Vercel</title>
    <style>
        :root {
            --system1-color: #4a6bdf;
            --system2-color: #8e44ad;
            --success-color: #27ae60;
            --warning-color: #e67e22;
            --danger-color: #e74c3c;
            --light-bg: #f8f9fa;
            --dark-text: #2c3e50;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--dark-text);
            background: linear-gradient(135deg, #f5f7fa 0%, #e6e9f0 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 40px;
            padding: 30px;
            background: linear-gradient(135deg, var(--system1-color), var(--system2-color));
            color: white;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .vercel-success {
            background: #000;
            color: white;
            padding: 25px;
            border-radius: 15px;
            margin: 30px 0;
            text-align: center;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
        }
        
        .vercel-success h3 {
            color: #6e8efb;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }
        
        .vercel-success h3:before {
            content: "▲";
            margin-right: 10px;
            font-size: 1.8rem;
        }
        
        .domain {
            font-family: monospace;
            background: #111;
            padding: 12px 20px;
            border-radius: 8px;
            margin: 15px 0;
            display: inline-block;
            font-size: 1.1rem;
            color: #6e8efb;
        }
        
        .deployment-info {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
        }
        
        .deployment-info h3 {
            color: var(--system1-color);
            margin-bottom: 15px;
            border-bottom: 2px solid var(--light-bg);
            padding-bottom: 10px;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .info-item {
            background: var(--light-bg);
            padding: 15px;
            border-radius: 8px;
        }
        
        .info-item h4 {
            color: var(--system2-color);
            margin-bottom: 8px;
            font-size: 0.9rem;
        }
        
        .systems-container {
            display: flex;
            gap: 30px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 40px;
        }
        
        .system {
            flex: 1;
            min-width: 350px;
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }
        
        .system:hover {
            transform: translateY(-5px);
        }
        
        .system-1 {
            border-top: 5px solid var(--system1-color);
        }
        
        .system-2 {
            border-top: 5px solid var(--system2-color);
        }
        
        .system-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-bg);
        }
        
        .system-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .system-1 .system-icon {
            background: var(--system1-color);
        }
        
        .system-2 .system-icon {
            background: var(--system2-color);
        }
        
        .system-title {
            font-size: 1.5rem;
        }
        
        .system-1 .system-title {
            color: var(--system1-color);
        }
        
        .system-2 .system-title {
            color: var(--system2-color);
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
        }
        
        input[type="text"] {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        input[type="text"]:focus {
            outline: none;
        }
        
        .system-1 input[type="text"]:focus {
            border-color: var(--system1-color);
        }
        
        .system-2 input[type="text"]:focus {
            border-color: var(--system2-color);
        }
        
        .btn {
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            margin-bottom: 15px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .system-1 .btn {
            background: var(--system1-color);
        }
        
        .system-1 .btn:hover {
            background: #3a5bce;
        }
        
        .system-2 .btn {
            background: var(--system2-color);
        }
        
        .system-2 .btn:hover {
            background: #793d97;
        }
        
        .data-container {
            background-color: var(--light-bg);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            min-height: 150px;
            border: 2px dashed #ddd;
        }
        
        .data-title {
            font-size: 1.1rem;
            margin-bottom: 10px;
            color: var(--dark-text);
            font-weight: 600;
        }
        
        .message {
            margin-top: 20px;
            padding: 15px;
            border-radius: 8px;
            display: none;
            animation: fadeIn 0.5s;
        }
        
        .success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .warning {
            background-color: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @media (max-width: 768px) {
            .systems-container {
                flex-direction: column;
            }
            
            .system {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>سیستەمی یەکگرتوو</h1>
            <p class="subtitle">هەدووکی یەکگرتوو بۆ ڕێگەپێدانی زانیاری ئالگۆریزمی</p>
        </header>
        
        <div class="vercel-success">
            <h3>دیپلۆی سەرکەوتوو لەسەر Vercel</h3>
            <p>سیستەمەکەت بە سەرکەوتوویی هۆست کراوە لەسەر Vercel</p>
            <div class="domain">faro-ruddy.vercel.app</div>
            <p>کە لە وێنەکەتدا دیاریکراوە و کاردەکات</p>
        </div>
        
        <div class="deployment-info">
            <h3>زانیاری دیپلۆی</h3>
            <div class="info-grid">
                <div class="info-item">
                    <h4>کاتی دیپلۆی</h4>
                    <p>١٨ چرکە</p>
                </div>
                <div class="info-item">
                    <h4>شوێن</h4>
                    <p>Washington, D.C., USA</p>
                </div>
                <div class="info-item">
                    <h4>Status</h4>
                    <p>سەرکەوتوو ✅</p>
                </div>
                <div class="info-item">
                    <h4>وەشان</h4>
                    <p>Vercel CLI 46.0.5</p>
                </div>
            </div>
        </div>
        
        <div class="systems-container">
            <div class="system system-1">
                <div class="system-header">
                    <div class="system-icon">1</div>
                    <h2 class="system-title">سیستەمی یەکەم</h2>
                </div>
                
                <div class="input-group">
                    <label for="dataInput">داتا بنێرە بۆ سیستەمی دووەم:</label>
                    <input type="text" id="dataInput" placeholder="داتا بنوسە ئێرە...">
                </div>
                
                <button class="btn" id="sendData">
                    <i>📤</i> ناردنی داتا
                </button>
                
                <div class="data-container">
                    <div class="data-title">داتای وەرگیراو لە سیستەمی دووەم:</div>
                    <div id="receivedData1">هێشتا داتایەک وەرنەگیراوە...</div>
                </div>
                
                <div class="message" id="system1Message"></div>
            </div>
            
            <div class="system system-2">
                <div class="system-header">
                    <div class="system-icon">2</div>
                    <h2 class="system-title">سیستەمی دووەم</h2>
                </div>
                
                <div class="data-container">
                    <div class="data-title">داتای وەرگیراو لە سیستەمی یەکەم:</div>
                    <div id="receivedData2">هێشتا داتایەک وەرنەگیراوە...</div>
                </div>
                
                <div class="input-group">
                    <label for="processedData">داتای پرۆسەکراو:</label>
                    <input type="text" id="processedData" readonly>
                </div>
                
                <button class="btn" id="processData">
                    <i>⚙️</i> پرۆسەکردنی داتا
                </button>
                
                <div class="message" id="system2Message"></div>
            </div>
        </div>
    </div>
    
    <script>
        // APIی ناوەکی بۆ پەیوەندیکردنی نێوان دوو سیستەمەکە
        const internalAPI = {
            data: null,
            processedData: null,
            
            // ناردنی داتا لە سیستەمی یەکەمەوە
            sendData: function(data) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        if (data && data.trim() !== '') {
                            this.data = {
                                value: data,
                                timestamp: new Date().toISOString(),
                                source: 'سیستەمی یەکەم'
                            };
                            resolve({ 
                                success: true, 
                                message: 'داتا بە سەرکەوتوویی نێردرا بۆ سیستەمی دووەم' 
                            });
                            
                            // نوێکردنەوەی سیستەمی دووەم
                            updateSystem2Data();
                        } else {
                            resolve({ 
                                success: false, 
                                message: 'تکایە داتا بنوسە بۆ ناردن!' 
                            });
                        }
                    }, 1000);
                });
            },
            
            // وەرگرتنی داتا لەلایەن سیستەمی دووەمەوە
            receiveData: function() {
                return this.data;
            },
            
            // ناردنی داتای پرۆسەکراو لە سیستەمی دووەمەوە
            sendProcessedData: function(processedData) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        if (processedData && processedData.trim() !== '') {
                            this.processedData = {
                                value: processedData,
                                timestamp: new Date().toISOString(),
                                source: 'سیستەمی دووەم'
                            };
                            resolve({ 
                                success: true, 
                                message: 'داتای پرۆسەکراو بە سەرکەوتوویی نێردرا' 
                            });
                            
                            // نوێکردنەوەی سیستەمی یەکەم
                            updateSystem1Data();
                        } else {
                            resolve({ 
                                success: false, 
                                message: 'هەڵە ڕوویدا لە پرۆسەکردنی داتا!' 
                            });
                        }
                    }, 1000);
                });
            },
            
            // وەرگرتنی داتای پرۆسەکراو لەلایەن سیستەمی یەکەمەوە
            receiveProcessedData: function() {
                return this.processedData;
            }
        };
        
        // فەنکشنی نوێکردنەوەی سیستەمی دووەم
        function updateSystem2Data() {
            const receivedData = internalAPI.receiveData();
            const receivedDataElement = document.getElementById('receivedData2');
            
            if (receivedData) {
                receivedDataElement.innerHTML = `
                    <strong>داتا:</strong> ${receivedData.value}<br>
                    <strong>سەرچاوە:</strong> ${receivedData.source}<br>
                    <strong>کات:</strong> ${new Date(receivedData.timestamp).toLocaleTimeString()}
                `;
            }
        }
        
        // فەنکشنی نوێکردنەوەی سیستەمی یەکەم
        function updateSystem1Data() {
            const processedData = internalAPI.receiveProcessedData();
            const receivedDataElement = document.getElementById('receivedData1');
            
            if (processedData) {
                receivedDataElement.innerHTML = `
                    <strong>داتا:</strong> ${processedData.value}<br>
                    <strong>سەرچاوە:</strong> ${processedData.source}<br>
                    <strong>کات:</strong> ${new Date(processedData.timestamp).toLocaleTimeString()}
                `;
            }
        }
        
        // فەنکشنی نیشاندانی پەیام
        function showMessage(element, message, type) {
            element.textContent = message;
            element.className = 'message ' + type;
            element.style.display = 'block';
            
            setTimeout(function() {
                element.style.display = 'none';
            }, 5000);
        }
        
        // دەستپێکردنی سیستەمەکان
        document.addEventListener('DOMContentLoaded', function() {
            const sendButton = document.getElementById('sendData');
            const processButton = document.getElementById('processData');
            const dataInput = document.getElementById('dataInput');
            const processedDataInput = document.getElementById('processedData');
            const system1Message = document.getElementById('system1Message');
            const system2Message = document.getElementById('system2Message');
            
            // ناردنی داتا لە سیستەمی یەکەمەوە
            sendButton.addEventListener('click', async function() {
                if (dataInput.value.trim() === '') {
                    showMessage(system1Message, 'تکایە داتا بنوسە بۆ ناردن!', 'error');
                    return;
                }
                
                sendButton.disabled = true;
                sendButton.innerHTML = '<i>⏳</i> ناردن...';
                
                const result = await internalAPI.sendData(dataInput.value);
                
                if (result.success) {
                    showMessage(system1Message, result.message, 'success');
                    dataInput.value = '';
                } else {
                    showMessage(system1Message, result.message, 'error');
                }
                
                sendButton.disabled = false;
                sendButton.innerHTML = '<i>📤</i> ناردنی داتا';
            });
            
            // پرۆسەکردنی داتا لە سیستەمی دووەمدا
            processButton.addEventListener('click', async function() {
                const dataToProcess = internalAPI.receiveData();
                
                if (!dataToProcess) {
                    showMessage(system2Message, 'هیچ داتایەک بۆ پرۆسەکردن نیە!', 'warning');
                    return;
                }
                
                processButton.disabled = true;
                processButton.innerHTML = '<i>⏳</i> پرۆسەکردن...';
                
                // ئالگۆرێزمی پرۆسەکردنی داتا
                const processedData = dataToProcess.value.toUpperCase() + ' [PROCESSED]';
                processedDataInput.value = processedData;
                
                const result = await internalAPI.sendProcessedData(processedData);
                
                if (result.success) {
                    showMessage(system2Message, result.message, 'success');
                } else {
                    showMessage(system2Message, result.message, 'error');
                }
                
                processButton.disabled = false;
                processButton.innerHTML = '<i>⚙️</i> پرۆسەکردنی داتا';
            });
        });
    </script>
</body>
</html>
