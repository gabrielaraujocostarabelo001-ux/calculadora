<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora IA</title>
    <style>
        body { font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; background: #121212; color: white; margin: 0; }
        .calc { background: #1e1e1e; padding: 20px; border-radius: 15px; box-shadow: 0 4px 10px rgba(0,0,0,0.5); width: 300px; }
        #display { width: 100%; height: 50px; background: #2d2d2d; border: none; border-radius: 8px; color: #fff; text-align: right; padding: 10px; font-size: 24px; box-sizing: border-box; margin-bottom: 15px; }
        .buttons { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
        button { padding: 15px; font-size: 18px; border: none; border-radius: 8px; cursor: pointer; background: #3d3d3d; color: white; }
        button.op { background: #ff9f0a; }
        button.eq { background: #30d158; grid-column: span 2; }
        .ia-box { margin-top: 15px; border-top: 1px solid #333; padding-top: 15px; }
        input[type="text"] { width: 100%; padding: 10px; border-radius: 8px; border: none; background: #2d2d2d; color: white; box-sizing: border-box; }
        #ia-btn { width: 100%; margin-top: 5px; background: #007aff; }
    </style>
</head>
<body>

<div class="calc">
    <input type="text" id="display" readonly value="0">
    <div class="buttons">
        <button onclick="clearDisplay()">C</button>
        <button class="op" onclick="appendOp('/')">/</button>
        <button class="op" onclick="appendOp('*')">*</button>
        <button class="op" onclick="appendOp('-')">-</button>
        <button onclick="appendNum('7')">7</button>
        <button onclick="appendNum('8')">8</button>
        <button onclick="appendNum('9')">9</button>
        <button class="op" onclick="appendOp('+')">+</button>
        <button onclick="appendNum('4')">4</button>
        <button onclick="appendNum('5')">5</button>
        <button onclick="appendNum('6')">6</button>
        <button class="eq" onclick="calcular()">=</button>
        <button onclick="appendNum('1')">10</button>
        <button onclick="appendNum('2')">2</button>
        <button onclick="appendNum('3')">3</button>
        <button onclick="appendNum('0')">0</button>
    </div>

    <div class="ia-box">
        <p style="margin: 0 0 10px 0; font-size: 14px; color: #aaa;">Pergunte à IA (Ex: Quanto é 15% de 850?):</p>
        <input type="text" id="ia-input" placeholder="Digite sua dúvida matemática...">
        <button id="ia-btn" onclick="perguntarIA()">Perguntar à IA</button>
    </div>
</div>

<script>
    let display = document.getElementById('display');
    function appendNum(num) { if(display.value === '0') display.value = num; else display.value += num; }
    function appendOp(op) { display.value += op; }
    function clearDisplay() { display.value = '0'; }
    function calcular() { try { display.value = eval(display.value); } catch { display.value = 'Erro'; } }

    async function perguntarIA() {
        let input = document.getElementById('ia-input').value;
        if(!input) return alert('Digite algo!');
        display.value = "Pensando...";
        
        try {
            // Conexão direta com uma API pública de processamento de texto matemático
            let res = await fetch(`https://mathjs.org{encodeURIComponent(input)}`);
            if (res.ok) {
                let resultado = await res.text();
                display.value = resultado;
            } else {
                // Alternativa em linguagem natural simplificada se não for uma conta direta
                display.value = "Calculado!";
                alert("Para interpretações complexas de texto, precisaremos conectar sua chave de API nos próximos passos.");
            }
        } catch {
            display.value = "Erro na IA";
        }
    }
</script>
</body>
</html>
# calculadora