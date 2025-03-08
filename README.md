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
        }

        .container {
            max-width: 900px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1 {
            text-align: center;
            color: #333;
        }

        .numbers-container {
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            gap: 10px;
            margin-top: 20px;
        }

        .number {
            background-color: #28a745;
            color: #fff;
            padding: 15px;
            text-align: center;
            border-radius: 8px;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .number.selected {
            background-color: #dc3545;
        }

        .number.disabled {
            background-color: #6c757d;
            cursor: not-allowed;
        }

        .cta-message {
            text-align: center;
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }

        .cta-button {
            display: block;
            width: 100%;
            padding: 15px;
            margin-top: 20px;
            background-color: #007bff;
            color: white;
            text-align: center;
            font-size: 18px;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .cta-button:hover {
            background-color: #0056b3;
        }

        .cta-button:active {
            background-color: #003d7a;
        }

        .number:active {
            transform: scale(1.1);
        }

    </style>
</head>

<body>
    <div class="container">
        <h1>Sorteio Rifa - Escolha seu Número</h1>
        <p class="cta-message">Escolha seu número do sorteio para participar do sorteio de um Kit Churrasco ou R$100 no Pix!</p>

        <div class="numbers-container" id="numbers-container">
            <!-- Os números serão gerados aqui pelo JavaScript -->
        </div>

        <button class="cta-button" id="confirmButton" disabled>Confirmar e Comprar Número</button>

        <p class="cta-message">Boa sorte e aproveite sua chance de ganhar!</p>
    </div>

    <script>
        const numbersContainer = document.getElementById('numbers-container');
        const confirmButton = document.getElementById('confirmButton');
        
        // Lista dos números já vendidos (esses números estarão bloqueados)
        const soldNumbers = [2, 3, 6, 7, 9, 10, 17, 18, 19, 21, 25, 27, 28, 29, 30, 31];

        // Lista dos números disponíveis (1 até 100)
        const availableNumbers = Array.from({ length: 100 }, (_, i) => i + 1);

        // Função para gerar os números
        function generateNumbers() {
            numbersContainer.innerHTML = '';  // Limpa o conteúdo atual

            availableNumbers.forEach(number => {
                const numberButton = document.createElement('div');
                numberButton.textContent = number;
                numberButton.classList.add('number');

                // Verifica se o número já foi vendido
                if (soldNumbers.includes(number)) {
                    numberButton.classList.add('disabled');
                    numberButton.setAttribute('disabled', 'true');
                }

                // Adiciona evento de clique para selecionar um número
                numberButton.addEventListener('click', () => {
                    if (!numberButton.classList.contains('disabled')) {
                        if (numberButton.classList.contains('selected')) {
                            numberButton.classList.remove('selected');
                            confirmButton.disabled = true;
                        } else {
                            // Marca como selecionado e ativa o botão de confirmação
                            numberButton.classList.add('selected');
                            confirmButton.disabled = false;
                        }
                    }
                });

                numbersContainer.appendChild(numberButton);
            });
        }

        // Função para enviar os dados para o WhatsApp
        function sendToWhatsApp(selectedNumber) {
            const name = prompt('Digite seu nome:');
            if (name) {
                const message = `Olá! Eu escolhi o número ${selectedNumber}. Meu nome é ${name}.`;
                const whatsappUrl = `https://wa.me/5521969054767?text=${encodeURIComponent(message)}`;
                window.open(whatsappUrl, '_blank');
            }
        }

        // Função que será chamada quando o botão "Confirmar" for clicado
        confirmButton.addEventListener('click', () => {
            const selectedNumber = document.querySelector('.number.selected');
            if (selectedNumber) {
                const number = selectedNumber.textContent;
                sendToWhatsApp(number);
            }
        });

        // Gera os números quando a página é carregada
        generateNumbers();
    </script>
</body>

</html>
