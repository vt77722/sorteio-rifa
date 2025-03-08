# sorteio-rifa
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sorteio Rifa - Escolha seu Número</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        h1 {
            background-color: #007bff;
            color: white;
            padding: 20px;
        }

        .cta {
            margin-top: 30px;
            padding: 10px;
            background-color: #28a745;
            color: white;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
        }

        .cta:hover {
            background-color: #218838;
        }

        .number-grid {
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            gap: 10px;
            justify-items: center;
            margin: 20px 0;
        }

        .number {
            background-color: #e9ecef;
            padding: 10px;
            font-size: 20px;
            cursor: pointer;
            border-radius: 5px;
            width: 60px;
            transition: background-color 0.3s;
        }

        .number.selected {
            background-color: #ffc107;
            cursor: not-allowed;
        }

        footer {
            margin-top: 50px;
            font-size: 14px;
            color: #6c757d;
        }
    </style>
</head>
<body>

<h1>Sorteio Rifa - Escolha seu Número</h1>

<p>Escolha seu número da sorte para participar do sorteio de um Kit Churrasco ou R$100 no Pix!</p>

<div class="number-grid">
    <!-- Números disponíveis -->
    <div class="number" id="num1" onclick="selectNumber(1)">1</div>
    <div class="number" id="num2" onclick="selectNumber(2)">2</div>
    <div class="number" id="num3" onclick="selectNumber(3)">3</div>
    <div class="number" id="num4" onclick="selectNumber(4)">4</div>
    <div class="number" id="num5" onclick="selectNumber(5)">5</div>
    <div class="number" id="num6" onclick="selectNumber(6)">6</div>
    <div class="number" id="num7" onclick="selectNumber(7)">7</div>
    <div class="number" id="num8" onclick="selectNumber(8)">8</div>
    <div class="number" id="num9" onclick="selectNumber(9)">9</div>
    <div class="number" id="num10" onclick="selectNumber(10)">10</div>
    <!-- Continue a lista de números até o 100 -->
</div>

<p><button class="cta" onclick="redirectToWhatsapp()">Confirmar e Comprar Número</button></p>

<footer>
    <p>Boa sorte e aproveite sua chance de ganhar!</p>
</footer>

<script>
    let selectedNumbers = [];

    function selectNumber(number) {
        const numElement = document.getElementById('num' + number);

        // Se o número já foi selecionado, não faz nada
        if (selectedNumbers.includes(number)) {
            alert('Este número já foi escolhido!');
            return;
        }

        // Seleciona ou desmarca o número
        numElement.classList.toggle('selected');
        
        if (numElement.classList.contains('selected')) {
            selectedNumbers.push(number);
        } else {
            selectedNumbers = selectedNumbers.filter(num => num !== number);
        }
    }

    function redirectToWhatsapp() {
        if (selectedNumbers.length === 0) {
            alert('Por favor, escolha um número!');
            return;
        }

        const whatsappMessage = `Olá! Eu escolhi os números: ${selectedNumbers.join(', ')}. Meu nome é [Seu Nome].`;
        const whatsappLink = `https://wa.me/5521969054767?text=${encodeURIComponent(whatsappMessage)}`;
        window.open(whatsappLink, '_blank');
    }
</script>

</body>
</html>
