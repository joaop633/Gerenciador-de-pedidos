<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gerenciador de Solicitações</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-image: url('URL_DA_IMAGEM'); /* Substitua pela URL da imagem */
            background-size: cover;
            background-position: center;
            color: white;
        }
        #pedidoForm {
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 5px;
            max-width: 400px;
            margin: auto;
            margin-top: 50px;
        }
        label, input, textarea {
            display: block;
            width: 100%;
            margin: 10px 0;
            padding: 10px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 3px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <form id="pedidoForm">
        <label for="numeroPedido">Número do Pedido:</label>
        <input type="text" id="numeroPedido" name="numeroPedido" required readonly>

        <label for="nomeCliente">Nome do Cliente:</label>
        <input type="text" id="nomeCliente" name="nomeCliente" required>

        <label for="telefone">Telefone:</label>
        <input type="tel" id="telefone" name="telefone" required>

        <label for="enderecoEntrega">Endereço de Entrega:</label>
        <input type="text" id="enderecoEntrega" name="enderecoEntrega" required>

        <label for="enderecoColeta">Endereço de Coleta:</label>
        <input type="text" id="enderecoColeta" name="enderecoColeta">

        <label for="observacao">Observação:</label>
        <textarea id="observacao" name="observacao"></textarea>

        <label for="valorEntrega">Valor da Entrega:</label>
        <input type="number" id="valorEntrega" name="valorEntrega" required>

        <button id="enviarWhatsApp" type="button">Enviar Pedido pelo WhatsApp</button>
    </form>

    <script>
        let numeroPedidoAtual = 0; // Inicializa a numeração em 0

        // Função para gerar o próximo número de pedido
        function gerarNumeroPedido() {
            if (numeroPedidoAtual < 99999) {
                numeroPedidoAtual++;
            } else {
                numeroPedidoAtual = 0; // Reinicia após 99999
            }
            document.getElementById('numeroPedido').value = numeroPedidoAtual;
        }

        // Chamar a função para gerar o número do pedido ao carregar a página
        window.onload = gerarNumeroPedido;

        document.getElementById('enviarWhatsApp').onclick = function() {
            const numero = '5553991036158'; // Número do WhatsApp
            const nome = document.getElementById('nomeCliente').value;
            const telefone = document.getElementById('telefone').value;
            const enderecoEntrega = document.getElementById('enderecoEntrega').value;
            const enderecoColeta = document.getElementById('enderecoColeta').value;
            const observacao = document.getElementById('observacao').value;
            const valorEntrega = document.getElementById('valorEntrega').value;

            const mensagem = `*Novo Pedido*\n` +
                             `Número do Pedido: ${numeroPedidoAtual}\n` +
                             `Nome: ${nome}\n` +
                             `Telefone: ${telefone}\n` +
                             `Endereço de Entrega: ${enderecoEntrega}\n` +
                             `Endereço de Coleta: ${enderecoColeta}\n` +
                             `Observação: ${observacao}\n` +
                             `Valor da Entrega: R$ ${valorEntrega}`;

            const urlWhatsApp = `https://api.whatsapp.com/send?phone=${numero}&text=${encodeURIComponent(mensagem)}`;
            
            window.open(urlWhatsApp, '_blank');
        };
    </script>

</body>
</html>
