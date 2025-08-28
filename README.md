<!DOCTYPE html>
<html lang="ku">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>سیستەمی یەکەم - هۆست لەسەر Vercel</title>
    <style>
        :root {
            --primary-color: #4a6bdf;
            --secondary-color: #8e44ad;
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
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: linear-gradient(135deg, var(--primary-color), #3a5bce);
            color: white;
            border-radius: 10px;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .host-address {
            display: inline-block;
            background: rgba(255, 255, 255, 0.2);
            padding: 5px 15px;
            border-radius: 20px;
            margin-top: 10px;
            font-family: monospace;
        }
        
        .vercel-info {
            background: #000;
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
            font-family: monospace;
        }
        
        .vercel-info h3 {
            color: #fff;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }
        
        .vercel-info h3:before {
            content: "▲";
            margin-right: 10px;
            color: #6e8efb;
        }
        
        .vercel-details {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
        }
        
        .vercel-detail {
            flex: 1;
            min-width: 200px;
            background: #111;
            padding: 10px;
            border-radius: 5px;
        }
        
        .vercel-detail h4 {
            color: #6e8efb;
            margin-bottom: 5px;
            font-size: 0.9rem;
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
            border-color: var(--primary-color);
            outline: none;
        }
        
        .btn {
            background: var(--primary-color);
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
            margin-bottom: 20px;
        }
        
        .btn:hover {
            background: #3a5bce;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .btn i {
            margin-right: 8px;
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
        
        .connection-status {
            text-align: center;
            margin: 20px 0;
            padding: 15px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
            border: 1px solid #eee;
        }
        
        .status-indicator {
            display: inline-block;
            width: 15px;
            height: 15px;
            border-radius: 50%;
            margin-right: 10px;
        }
        
        .status-connected {
            background: var(--success-color);
        }
        
        .api-info {
            background: var(--light-bg);
            padding: 20px;
            border-radius: 10px;
            margin-top: 25px;
        }
        
        .api-info h2 {
            color: var(--primary-color);
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.3rem;
        }
        
        .api-details {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
        }
        
        .api-card {
            flex: 1;
            min-width: 200px;
            background: white;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
        }
        
        .api-card h3 {
            color: var(--secondary-color);
            margin-bottom: 10px;
            font-size: 1rem;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .api-details, .vercel-details {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>سیستەمی یەکەم</h1>
            <p class="subtitle">ناردنی داتا بۆ سیستەمی دووەم</p>
            <div class="host-address">هۆست لەسەر Vercel</div>
        </header>
        
        <div class="vercel-info">
            <h3>Vercel Deployment</h3>
            <p>ئەم سیستەمە هۆست کراوە لەسەر Vercel</p>
            <div class="vercel-details">
                <div class="vercel-detail">
                    <h4>ناونیشانی ماڵپەڕ</h4>
                    <p>faro-ruddy.vercel.app</p>
                </div>
                <div class="vercel-detail">
                    <h4>Status</h4>
                    <p>Ready ✅</p>
                </div>
                <div class="vercel-detail">
                    <h4>کاتی ئامادەبوون</h4>
                    <p>3s</p>
                </div>
            </div>
        </div>
        
        <div class="connection-status">
            <h3><span class="status-indicator status-connected"></span>پەیوەندی دەستپێکراوە</h3>
            <p>ئامادەیە بۆ ناردنی داتا بۆ سیستەمی دووەم</p>
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
            <div id="receivedData">هێشتا داتایەک وەرنەگیراوە...</div>
        </div>
        
        <div class="message" id="systemMessage"></div>
        
        <div class="api-info">
            <h2>ڕێگەی پەیوەندیکردن</h2>
            <div class="api-details">
                <div class="api-card">
                    <h3>ڕێگە</h3>
                    <p>POST /api/data</p>
                </div>
                <div class="api-card">
                    <h3>شێوازی داتا</h3>
                    <p>JSON</p>
                </div>
                <div class="api-card">
                    <h3>Authentication</h3>
                    <p>Bearer Token</p>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // APIی ساختەی بۆ نیشاندانی کارلێک لەگەڵ سیستەمی دووەم
        const mockAPI = {
            // ناردنی داتا بۆ سیستەمی دووەم
            sendData: function(data) {
                return new Promise((resolve) => {
                    // لە ڕێالیدا، ئەمە POST requestێکە بۆ APIەکەی سیستەمی دووەم
                    setTimeout(() => {
                        if (Math.random() > 0.2) { // 80% chance of success
                            // لە ڕێالیدا، ئەمە وەڵامێکی JSONە لە سێرڤەرەوە
                            resolve({ 
                                success: true, 
                                message: 'داتا بە سەرکەوتوویی نێردرا بۆ سیستەمی دووەم',
                                received: false // لەم سیستەمە تەنها ناردنە
                            });
                        } else {
                            resolve({ 
                                success: false, 
                                message: 'هەڵە ڕوویدا لە ناردنی داتا! پەیوەندی پێکن بە سیستەمی دووەمەوە'
                            });
                        }
                    }, 1500); // درەنگکردنی ساختەیی
                });
            },
            
            // وەرگرتنی داتا لە سیستەمی دووەم (لە ڕێالیدا ئەمە Webhook یان polling یان SSE یان WebSocket دەبێت)
            checkForProcessedData: function() {
                // لەم نموونەیە، بە شێوەیەکی ساختەیی داتا دەگەڕێنێتەوە
                if (Math.random() > 0.7) { // 30% chance of having data
                    return {
                        value: `پڕۆسەکراو: ${Math.random().toString(36).substring(2, 10).toUpperCase()}`,
                        source: 'سیستەمی دووەم',
                        timestamp: new Date().toISOString()
                    };
                }
                return null;
            }
        };
        
        // دەستپێکردنی سیستەم
        document.addEventListener('DOMContentLoaded', function() {
            const sendButton = document.getElementById('sendData');
            const dataInput = document.getElementById('dataInput');
            const receivedData = document.getElementById('receivedData');
            const systemMessage = document.getElementById('systemMessage');
            
            // ناردنی داتا بۆ سیستەمی دووەم
            sendButton.addEventListener('click', async function() {
                if (dataInput.value.trim() === '') {
                    showMessage(systemMessage, 'تکایە داتا بنوسە بۆ ناردن!', 'error');
                    return;
                }
                
                sendButton.disabled = true;
                sendButton.innerHTML = '<i>⏳</i> ناردن...';
                
                // ناردنی داتا بۆ سیستەمی دووەم
                const result = await mockAPI.sendData(dataInput.value);
                
                if (result.success) {
                    showMessage(systemMessage, result.message, 'success');
                    dataInput.value = '';
                } else {
                    showMessage(systemMessage, result.message, 'error');
                }
                
                sendButton.disabled = false;
                sendButton.innerHTML = '<i>📤</i> ناردنی داتا';
            });
            
            // پشکنینی بۆ داتای پرۆسەکراو لە سیستەمی دووەم (لە ڕێالیدا بە Webhook یان polling)
            setInterval(() => {
                const processedData = mockAPI.checkForProcessedData();
                if (processedData) {
                    receivedData.innerHTML = `<strong>داتا:</strong> ${processedData.value}<br>
                                              <strong>سەرچاوە:</strong> ${processedData.source}<br>
                                              <strong>کات:</strong> ${new Date(processedData.timestamp).toLocaleTimeString()}`;
                }
            }, 3000);
            
            // فەنکشنی نیشاندانی پەیام
            function showMessage(element, message, type) {
                element.textContent = message;
                element.className = 'message ' + type;
                element.style.display = 'block';
                
                // لەکارکەوتنی پەیام دوای ماوەیەک
                setTimeout(function() {
                    element.style.display = 'none';
                }, 5000);
            }
        });
    </script>
</body>
</html>
