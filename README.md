<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>巧克力电池充电时间计算器</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #2c3e50);
            color: #333;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .container {
            max-width: 1200px;
            width: 100%;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            padding: 20px 0 30px;
            color: white;
        }
        
        h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.3);
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            color: #ddd;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .card {
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0,0,0,0.4);
            overflow: hidden;
            margin-bottom: 30px;
        }
        
        .calculator-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            padding: 30px;
        }
        
        @media (max-width: 900px) {
            .calculator-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .input-section {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
        }
        
        .section-title {
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .input-group {
            margin-bottom: 20px;
            position: relative;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #2c3e50;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        input, select {
            width: 100%;
            padding: 14px 15px;
            border: 2px solid #ddd;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s;
            background: #fff;
        }
        
        input:focus, select:focus {
            border-color: #3498db;
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        
        .btn-container {
            display: flex;
            gap: 15px;
            margin-top: 10px;
        }
        
        button {
            flex: 1;
            padding: 15px;
            font-size: 18px;
            font-weight: 600;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
            border: none;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }
        
        .calculate-btn {
            background: linear-gradient(to right, #3498db, #2c3e50);
            color: white;
        }
        
        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .reset-btn {
            background: #e74c3c;
            color: white;
        }
        
        .results {
            padding: 25px;
            background: #f0f8ff;
            border-radius: 15px;
            margin: 20px;
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .result-card {
            background: linear-gradient(135deg, #3498db, #2c3e50);
            border-radius: 15px;
            padding: 25px 20px;
            color: white;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            transition: transform 0.3s;
        }
        
        .result-card:hover {
            transform: translateY(-5px);
        }
        
        .result-card h3 {
            font-size: 1.1rem;
            margin-bottom: 15px;
            opacity: 0.9;
        }
        
        .result-value {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 5px;
        }
        
        .result-unit {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .formula-section {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            margin: 20px;
        }
        
        .formula-box {
            background: #e3f2fd;
            border-radius: 10px;
            padding: 20px;
            font-family: 'Courier New', monospace;
            font-size: 18px;
            margin: 20px 0;
            border-left: 4px solid #3498db;
        }
        
        .formula-explanation {
            margin-top: 20px;
            padding-left: 20px;
            border-left: 3px solid #34dbd8;
        }
        
        .formula-explanation li {
            margin-bottom: 10px;
            line-height: 1.6;
        }
        
        footer {
            text-align: center;
            color: white;
            padding: 20px;
            font-size: 0.9rem;
            opacity: 0.8;
            margin-top: 20px;
        }
        
        .soc-section {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            margin: 20px;
        }
        
        .soc-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .soc-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .soc-table th {
            background: #3498db;
            color: white;
            padding: 12px;
            text-align: center;
        }
        
        .soc-table td {
            padding: 12px;
            text-align: center;
            border-bottom: 1px solid #eee;
        }
        
        .soc-table tr:nth-child(even) {
            background: #f8f9fa;
        }
        
        .soc-table tr:last-child td {
            border-bottom: none;
        }
        
        .soc-table tfoot tr {
            background: #2c3e50 !important;
            color: white;
            font-weight: bold;
        }
        
        .soc-table tfoot td {
            padding: 15px;
            font-size: 1.1rem;
        }
        
        .highlight {
            background-color: #fffde7 !important;
            font-weight: bold;
        }
        
        .error-message {
            color: #e74c3c;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 0.5s ease-in-out;
        }
        
        .summary-row {
            background: #2c3e50;
            color: white;
            font-weight: bold;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .status-active {
            background-color: #2ecc71;
            box-shadow: 0 0 8px #2ecc71;
        }
        
        .status-inactive {
            background-color: #95a5a6;
        }
        
        .calculation-log {
            background: #f1f8e9;
            border-radius: 10px;
            padding: 15px;
            margin-top: 20px;
            font-family: monospace;
            font-size: 14px;
            max-height: 150px;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-battery-full"></i> 巧克力电池充电时间计算器</h1>
            <p class="subtitle">基于SOC分段充电模型设计 | 精确计算不同SOC区间的充电时间</p>
        </header>
        
        <div class="card">
            <div class="calculator-grid">
                <div class="input-section">
                    <h2 class="section-title"><i class="fas fa-car-battery"></i> 电池参数</h2>
                    
                    <div class="input-group">
                        <label for="battery-capacity"><i class="fas fa-car-battery"></i> 电池容量 (Ah)</label>
                        <input type="number" id="battery-capacity" placeholder="例如：200" min="1" value="100">
                        <div class="error-message" id="capacity-error"></div>
                    </div>
                    
                    <div class="input-group">
                        <label for="system-voltage"><i class="fas fa-bolt"></i> 系统电压 (V)</label>
                        <input type="number" id="system-voltage" placeholder="例如：367" min="1" value="367">
                        <div class="error-message" id="voltage-error"></div>
                    </div>
                    
                    <div class="input-group">
                        <label for="initial-soc"><i class="fas fa-battery-quarter"></i> 初始 SOC (%)</label>
                        <input type="number" id="initial-soc" placeholder="0-100" min="0" max="100" value="30">
                        <div class="error-message" id="initial-soc-error"></div>
                    </div>
                    
                    <div class="input-group">
                        <label for="target-soc"><i class="fas fa-battery-full"></i> 目标 SOC (%)</label>
                        <input type="number" id="target-soc" placeholder="0-100" min="0" max="100" value="80">
                        <div class="error-message" id="target-soc-error"></div>
                    </div>
                </div>
                
                <div class="input-section">
                    <h2 class="section-title"><i class="fas fa-charging-station"></i> 充电参数</h2>
                    
                    <div class="input-group">
                        <label for="charger-power"><i class="fas fa-bolt"></i> 充电机功率 (kW)</label>
                        <input type="number" id="charger-power" placeholder="例如：50" min="1" value="50">
                        <div class="error-message" id="power-error"></div>
                    </div>
                    
                    <div class="input-group">
                        <label for="charging-efficiency"><i class="fas fa-tachometer-alt"></i> 充电效率 (%)</label>
                        <input type="number" id="charging-efficiency" placeholder="例如：95" min="1" max="100" value="95">
                        <div class="error-message" id="efficiency-error"></div>
                    </div>
                    
                    <div class="input-group">
                        <label for="soc-segments"><i class="fas fa-layer-group"></i> SOC分段模式</label>
                        <select id="soc-segments">
                            <option value="single">单段充电（整体计算）</option>
                            <option value="multi" selected>多段充电（SOC分段计算）</option>
                        </select>
                    </div>
                    
                    <div class="btn-container">
                        <button id="calculate-btn" class="calculate-btn">
                            <i class="fas fa-calculator"></i> 计算充电时间
                        </button>
                        <button id="reset-btn" class="reset-btn">
                            <i class="fas fa-redo"></i> 重置
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="results">
                <h2 class="section-title"><i class="fas fa-chart-line"></i> 计算结果</h2>
                
                <div class="results-grid">
                    <div class="result-card">
                        <h3>电池总能量</h3>
                        <div class="result-value" id="total-energy">36.70</div>
                        <div class="result-unit">kWh</div>
                    </div>
                    <div class="result-card">
                        <h3>需要充入能量</h3>
                        <div class="result-value" id="required-energy">18.35</div>
                        <div class="result-unit">kWh</div>
                    </div>
                    <div class="result-card">
                        <h3>理论充电时间</h3>
                        <div class="result-value" id="charging-time">0.39</div>
                        <div class="result-unit">小时</div>
                    </div>
                    <div class="result-card">
                        <h3>实际充电时间</h3>
                        <div class="result-value" id="actual-time">0.45</div>
                        <div class="result-unit">小时</div>
                    </div>
                </div>
                
                <div class="calculation-log">
                    <p><span class="status-indicator status-active"></span> 计算状态: <span id="calc-status">就绪</span></p>
                    <p><span class="status-indicator status-inactive"></span> 最后计算: <span id="last-calc">-</span></p>
                    <p><span class="status-indicator status-inactive"></span> 计算详情: <span id="calc-details">等待计算...</span></p>
                </div>
            </div>
            
            <div class="soc-section">
                <h2 class="section-title"><i class="fas fa-layer-group"></i> SOC分段充电数据</h2>
                
                <table class="soc-table">
                    <thead>
                        <tr>
                            <th>SOC范围</th>
                            <th>充电电压 (V)</th>
                            <th>充电时长 (分钟)</th>
                            <th>充电电量 (kWh)</th>
                            <th>充电功率 (kW)</th>
                            <th>充电电流 (A)</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr id="segment-0-30">
                            <td>0-30%</td>
                            <td>367</td>
                            <td>14.17</td>
                            <td>16.8</td>
                            <td>71.14</td>
                            <td>196</td>
                        </tr>
                        <tr id="segment-30-80" class="highlight">
                            <td>30-80%</td>
                            <td>367</td>
                            <td>23.62</td>
                            <td>28.0</td>
                            <td>71.12</td>
                            <td>194</td>
                        </tr>
                        <tr id="segment-80-100">
                            <td>80-100%</td>
                            <td>367</td>
                            <td>24.06</td>
                            <td>11.2</td>
                            <td>27.90</td>
                            <td>76</td>
                        </tr>
                    </tbody>
                    <tfoot>
                        <tr class="summary-row">
                            <td colspan="2">充电时长汇总</td>
                            <td id="summary-minutes">23.62</td>
                            <td colspan="3">分钟 | 实际充电时间: <span id="summary-actual">0.45</span> 小时</td>
                        </tr>
                    </tfoot>
                </table>
            </div>
            
            <div class="formula-section">
                <h2 class="section-title"><i class="fas fa-calculator"></i> 充电时间计算公式</h2>
                <div class="formula-box">
                    充电时间 (小时) = [电池容量 (Ah) × 系统电压 (V) × (目标SOC - 初始SOC) / 100] / [充电机功率 (kW) × (充电效率 / 100)]
                </div>
                <div class="formula-explanation">
                    <h3>计算步骤说明：</h3>
                    <ul>
                        <li><strong>计算电池总能量 (kWh):</strong> 电池容量 (Ah) × 系统电压 (V) / 1000</li>
                        <li><strong>计算需要充入的能量 (kWh):</strong> 电池总能量 × (目标SOC - 初始SOC) / 100</li>
                        <li><strong>计算有效充电功率 (kW):</strong> 充电机功率 × (充电效率 / 100)</li>
                        <li><strong>计算充电时间 (小时):</strong> 需要充入能量 / 有效充电功率</li>
                        <li><strong>实际充电时间:</strong> 理论充电时间 × 安全系数 (1.15，考虑实际损耗)</li>
                    </ul>
                </div>
            </div>
        </div>
        
        <footer>
            <p>© 2025 巧克力电池充电时间计算模型 | 基于SOC分段充电数据设计 | V1.0版</p>
        </footer>
    </div>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const calculateBtn = document.getElementById('calculate-btn');
            const resetBtn = document.getElementById('reset-btn');
            const socSegments = document.getElementById('soc-segments');
            
            // 初始显示
            updateStatus('就绪', '等待用户输入');
            
            // 计算按钮事件
            calculateBtn.addEventListener('click', function() {
                updateStatus('计算中...', '正在处理输入参数');
                setTimeout(calculateChargingTime, 500);
            });
            
            // 重置按钮事件
            resetBtn.addEventListener('click', function() {
                document.getElementById('battery-capacity').value = '152';
                document.getElementById('system-voltage').value = '367';
                document.getElementById('initial-soc').value = '10';
                document.getElementById('target-soc').value = '90';
                document.getElementById('charger-power').value = '80';
                document.getElementById('charging-efficiency').value = '95';
                socSegments.value = 'multi';
                
                // 清除错误信息
                document.querySelectorAll('.error-message').forEach(el => {
                    el.style.display = 'none';
                    el.textContent = '';
                });
                
                updateStatus('已重置', '所有参数已恢复默认值');
                setTimeout(calculateChargingTime, 300);
            });
            
            // SOC分段选择事件
            socSegments.addEventListener('change', function() {
                const mode = this.value === 'multi' ? '多段充电模式' : '单段充电模式';
                updateStatus('模式变更', `已切换到${mode}`);
                calculateChargingTime();
            });
            
            // 输入验证
            document.querySelectorAll('input').forEach(input => {
                input.addEventListener('input', function() {
                    const id = this.id;
                    const errorElement = document.getElementById(`${id}-error`);
                    
                    if (this.value === '') {
                        errorElement.textContent = '此字段不能为空';
                        errorElement.style.display = 'block';
                    } else {
                        errorElement.style.display = 'none';
                    }
                    
                    // 特定字段验证
                    if (id === 'initial-soc' || id === 'target-soc') {
                        const value = parseFloat(this.value);
                        if (isNaN(value) || value < 0 || value > 100) {
                            errorElement.textContent = 'SOC值必须在0-100之间';
                            errorElement.style.display = 'block';
                        }
                    }
                    
                    // 自动计算
                    if (this.value && !errorElement.textContent) {
                        calculateChargingTime();
                    }
                });
            });
            
            // 更新状态函数
            function updateStatus(status, details) {
                document.getElementById('calc-status').textContent = status;
                document.getElementById('calc-details').textContent = details;
                document.getElementById('last-calc').textContent = new Date().toLocaleTimeString();
                
                // 更新状态指示器
                const indicators = document.querySelectorAll('.status-indicator');
                indicators.forEach(indicator => {
                    indicator.classList.remove('status-active');
                    indicator.classList.add('status-inactive');
                });
                
                if (status !== '就绪') {
                    document.querySelector('.status-indicator').classList.remove('status-inactive');
                    document.querySelector('.status-indicator').classList.add('status-active');
                }
            }
            
            // 计算充电时间函数（已修复）
            function calculateChargingTime() {
                // 获取输入值
                const batteryCapacity = parseFloat(document.getElementById('battery-capacity').value) || 100;
                const systemVoltage = parseFloat(document.getElementById('system-voltage').value) || 367;
                const initialSOC = parseFloat(document.getElementById('initial-soc').value) || 30;
                const targetSOC = parseFloat(document.getElementById('target-soc').value) || 80;
                const chargerPower = parseFloat(document.getElementById('charger-power').value) || 50;
                const efficiency = parseFloat(document.getElementById('charging-efficiency').value) || 95;
                const segmentMode = document.getElementById('soc-segments').value;
                
                // 验证输入
                let hasError = false;
                const errors = [];
                
                if (isNaN(batteryCapacity) || batteryCapacity <= 0) {
                    document.getElementById('capacity-error').textContent = '请输入有效的电池容量';
                    document.getElementById('capacity-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的电池容量');
                } else {
                    document.getElementById('capacity-error').style.display = 'none';
                }
                
                if (isNaN(systemVoltage) || systemVoltage <= 0) {
                    document.getElementById('voltage-error').textContent = '请输入有效的系统电压';
                    document.getElementById('voltage-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的系统电压');
                } else {
                    document.getElementById('voltage-error').style.display = 'none';
                }
                
                if (isNaN(initialSOC) || initialSOC < 0 || initialSOC > 100) {
                    document.getElementById('initial-soc-error').textContent = '初始SOC必须在0.1-100之间';
                    document.getElementById('initial-soc-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的初始SOC');
                } else {
                    document.getElementById('initial-soc-error').style.display = 'none';
                }
                
                if (isNaN(targetSOC) || targetSOC < 0 || targetSOC > 100) {
                    document.getElementById('target-soc-error').textContent = '目标SOC必须在0-100之间';
                    document.getElementById('target-soc-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的目标SOC');
                } else {
                    document.getElementById('target-soc-error').style.display = 'none';
                }
                
                if (initialSOC >= targetSOC) {
                    document.getElementById('target-soc-error').textContent = '目标SOC必须大于初始SOC';
                    document.getElementById('target-soc-error').style.display = 'block';
                    hasError = true;
                    errors.push('目标SOC必须大于初始SOC');
                } else {
                    document.getElementById('target-soc-error').style.display = 'none';
                }
                
                if (isNaN(chargerPower) || chargerPower <= 0) {
                    document.getElementById('power-error').textContent = '充电机功率必须大于0';
                    document.getElementById('power-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的充电机功率');
                } else {
                    document.getElementById('power-error').style.display = 'none';
                }
                
                if (isNaN(efficiency) || efficiency <= 0 || efficiency > 100) {
                    document.getElementById('efficiency-error').textContent = '充电效率必须在1-100之间';
                    document.getElementById('efficiency-error').style.display = 'block';
                    hasError = true;
                    errors.push('无效的充电效率');
                } else {
                    document.getElementById('efficiency-error').style.display = 'none';
                }
                
                if (hasError) {
                    updateStatus('计算失败', '输入参数错误: ' + errors.join(', '));
                    return;
                }
                
                // 计算电池总能量 (kWh)
                const totalEnergy = (batteryCapacity * systemVoltage) / 1000;
                
                // 计算需要充入的能量 (kWh)
                const socDifference = (targetSOC - initialSOC) / 100;
                const requiredEnergy = totalEnergy * socDifference;
                
                // 计算有效充电功率 (kW)
                const effectivePower = chargerPower * (efficiency / 100);
                
                // 计算充电时间 (小时)
                let chargingTime;
                let actualChargingTime;
                let modeText = '';
                
                if (segmentMode === 'multi') {
                    // SOC分段计算逻辑
                    const segmentResult = calculateSegmentTime(initialSOC, targetSOC, totalEnergy);
                    chargingTime = segmentResult.totalTime;
                    actualChargingTime = chargingTime * 1.15;
                    modeText = '使用分段充电模式';
                    
                    // 更新表格中的分段数据
                    updateSegmentData(segmentResult.segments);
                } else {
                    // 单段计算逻辑
                    chargingTime = requiredEnergy / effectivePower;
                    actualChargingTime = chargingTime * 1.15;
                    modeText = '使用单段充电模式';
                }
                
                // 显示结果
                document.getElementById('total-energy').textContent = totalEnergy.toFixed(2);
                document.getElementById('required-energy').textContent = requiredEnergy.toFixed(2);
                document.getElementById('charging-time').textContent = chargingTime.toFixed(2);
                document.getElementById('actual-time').textContent = actualChargingTime.toFixed(2);
                
                // 更新汇总行
                updateSummary(chargingTime, actualChargingTime);
                
                // 高亮当前SOC分段
                highlightCurrentSegment(initialSOC, targetSOC);
                
                // 添加动画效果
                document.querySelectorAll('.result-card').forEach(card => {
                    card.classList.add('pulse');
                    setTimeout(() => card.classList.remove('pulse'), 500);
                });
                
                // 更新状态
                updateStatus('计算完成', 
                    `电池: ${batteryCapacity}Ah, 电压: ${systemVoltage}V, SOC: ${initialSOC}% → ${targetSOC}% | ${modeText}`
                );
            }
            
            // SOC分段计算函数
            function calculateSegmentTime(initialSOC, targetSOC, totalEnergy) {
                // 定义SOC分段和对应的充电功率
                const segments = [
                    { min: 0, max: 30, power: 71.14 },
                    { min: 30, max: 80, power: 71.12 },
                    { min: 80, max: 100, power: 27.90 }
                ];
                
                let totalTime = 0;
                const segmentDetails = [];
                
                // 遍历每个分段
                for (const segment of segments) {
                    // 如果充电范围与当前分段有重叠
                    if (initialSOC < segment.max && targetSOC > segment.min) {
                        // 计算当前分段内的起始和结束SOC
                        const segmentStart = Math.max(initialSOC, segment.min);
                        const segmentEnd = Math.min(targetSOC, segment.max);
                        
                        // 计算当前分段需要充入的能量
                        const segmentSocDiff = (segmentEnd - segmentStart) / 100;
                        const segmentEnergy = totalEnergy * segmentSocDiff;
                        
                        // 计算当前分段所需时间
                        const segmentTime = segmentEnergy / segment.power;
                        
                        // 累加到总时间
                        totalTime += segmentTime;
                        
                        // 保存分段详情
                        segmentDetails.push({
                            range: `${segment.min}-${segment.max}%`,
                            start: segmentStart,
                            end: segmentEnd,
                            energy: segmentEnergy,
                            time: segmentTime,
                            power: segment.power
                        });
                    }
                }
                
                return {
                    totalTime: totalTime,
                    segments: segmentDetails
                };
            }
            
            // 更新分段数据
            function updateSegmentData(segments) {
                // 重置所有行
                document.getElementById('segment-0-30').style.display = 'table-row';
                document.getElementById('segment-30-80').style.display = 'table-row';
                document.getElementById('segment-80-100').style.display = 'table-row';
                
                // 更新每行的数据
                segments.forEach(segment => {
                    let rowId = '';
                    if (segment.range === '0-30%') rowId = 'segment-0-30';
                    if (segment.range === '30-80%') rowId = 'segment-30-80';
                    if (segment.range === '80-100%') rowId = 'segment-80-100';
                    
                    if (rowId) {
                        const row = document.getElementById(rowId);
                        if (row) {
                            row.cells[2].textContent = (segment.time * 60).toFixed(2);
                            row.cells[3].textContent = segment.energy.toFixed(1);
                        }
                    }
                });
            }
            
            // 更新汇总行
            function updateSummary(chargingTime, actualChargingTime) {
                const minutes = Math.round(chargingTime * 60);
                document.getElementById('summary-minutes').textContent = minutes;
                document.getElementById('summary-actual').textContent = actualChargingTime.toFixed(2);
            }
            
            // 高亮当前SOC分段
            function highlightCurrentSegment(initialSOC, targetSOC) {
                // 清除所有高亮
                document.querySelectorAll('.soc-table tr').forEach(row => {
                    row.classList.remove('highlight');
                });
                
                // 确定当前所在的SOC分段
                let segmentId = '';
                if (initialSOC < 30 && targetSOC > 0) {
                    segmentId = 'segment-0-30';
                } else if (initialSOC < 80 && targetSOC > 30) {
                    segmentId = 'segment-30-80';
                } else if (initialSOC < 100 && targetSOC > 80) {
                    segmentId = 'segment-80-100';
                }
                
                // 应用高亮
                if (segmentId) {
                    const segmentRow = document.getElementById(segmentId);
                    if (segmentRow) {
                        segmentRow.classList.add('highlight');
                    }
                }
            }
            
            // 初始计算
            calculateChargingTime();
        });
    </script>
</body>
</html>
